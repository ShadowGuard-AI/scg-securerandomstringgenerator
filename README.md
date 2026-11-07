# scg-SecureRandomStringGenerator
Generates cryptographically secure random strings of specified length, allowing users to specify the character set (alphanumeric, special characters, etc.). Provides a command-line interface to generate strings and securely copy them to the clipboard. Plain generation uses only the standard library. The `pyperclip` and `jinja2` packages are imported only by the clipboard and template paths that use them. With `--template`, the generated string is rendered into a Jinja2 template file supplied by the user and the rendered output is printed.

A custom character set is deduplicated, keeping first occurrence order, before generating, so repeating a character does not weight the output.

With `--hash_password`, the generated string itself is never printed. The output is a salted derivation in the format `pbkdf2_sha256$200000$<salt hex>$<digest hex>`, using PBKDF2-HMAC-SHA256 with 200,000 iterations and a random salt from `secrets`, so the result can be verified later from the salt and iteration count. `--hash_password` and `--template` cannot be used together. With `--copy` in the hash branch, the derived hash value is copied, not the generated string.

A generation or template failure exits 1 and prints no string. A clipboard failure is only a warning: the generated string is still printed and the run still exits 0.

## Install
`git clone https://github.com/ShadowGuard-AI/scg-securerandomstringgenerator`
`pip install -r requirements.txt`

## Usage
`python3 main.py [-l LENGTH] [-c CHARSET] [--custom_chars CUSTOM_CHARS] [--copy] [--template TEMPLATE] [--hash_password]`

## Parameters
- `-l, --length`: Length of the random string (default: 16).
- `-c, --charset`: Character set to use: alphanumeric, alphanumeric_symbols, digits, letters, symbols, or custom (default: alphanumeric).
- `--custom_chars`: Custom character set to use when --charset is set to custom. Required in that case.
- `--copy`: Copy the generated string to the clipboard. With --hash_password, copies the derived hash value instead.
- `--template`: Path to Jinja2 template file for code generation.
- `--hash_password`: Derive a salted hash of the generated string with PBKDF2-HMAC-SHA256 (200,000 iterations and a random salt). The generated string itself is not printed in this branch.

## License
MIT License. See LICENSE.
