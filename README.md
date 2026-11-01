# scg-SecureRandomStringGenerator
Generates cryptographically secure random strings of specified length, allowing users to specify the character set (alphanumeric, special characters, etc.). Provides a command-line interface to generate strings and securely copy them to the clipboard. Plain generation uses only the standard library. The `pyperclip` and `jinja2` packages are imported only by the clipboard and template paths that use them. - Focused on Automates the generation of basic secure code snippets (e.g., password hashing, input validation, secure random number generation) using Jinja2 templates and a set of predefined secure coding practices. Facilitates quick and consistent security implementation.

A custom character set is deduplicated, keeping first occurrence order, before generating, so repeating a character does not weight the output.

With `--hash_password`, the generated string itself is never printed. The output is a salted derivation in the format `pbkdf2_sha256$200000$<salt hex>$<digest hex>`, using PBKDF2-HMAC-SHA256 with 200,000 iterations and a random salt from `secrets`, so the result can be verified later from the salt and iteration count. `--hash_password` and `--template` cannot be used together. With `--copy` in the hash branch, the derived hash value is copied, not the generated string.

A generation or template failure exits 1 and prints no string.

## Install
`git clone https://github.com/ShadowStrikeHQ/scg-securerandomstringgenerator`
`pip install -r requirements.txt`

## Usage
`./scg-securerandomstringgenerator [params]`

## Parameters
- `-l`: No description provided
- `-c`: Character set to use:\n
- `--custom_chars`: Custom character set to use when --charset is set to
- `--copy`: Copy the generated string to the clipboard.
- `--template`: Path to Jinja2 template file for code generation.
- `--hash_password`: No description provided

## License
Copyright (c) ShadowStrikeHQ
