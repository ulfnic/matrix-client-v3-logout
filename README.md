# matrix-logout

`curl` wrapper for using an access token to logout of a matrix homeserver.

```bash
# Logout
matrix-logout -u 'myuser' -T <(printf '%s' 'myaccesstoken') 'https://myhomeserver.org'
```
```bash
# stdout
{}
```
---
```bash
# Output help
matrix-logout --help
```
```bash
matrix-logout [ARGUEMENT...] [--] [HOMESERVER]

curl wrapper for using an access_token to logout of a matrix homeserver.

DEPENDENCIES
	curl

ARGUEMENT
	-T|--access-token-file ACCESS_TOKEN_FILE   See: ACCESS_TOKEN_FILE
	-U|--user-file USER_FILE                   See: USER_FILE
	--dry-run                                  Do everything except send the request
	--debug                                    Output debugging information
	-h|--help                                  Print help doc
	HOMESERVER                                 Homeserver base url

ACCESS_TOKEN_FILE
	Path to a file containing an access token on the first line. Additional lines are ignored.
	If the path is a hyphen (-), path becomes stdin.

USER_FILE
	Path to a file containing VALUE_PAIRs as an alternative to using ARGUEMENTs, ex:
		VAR_NAME=VALUE
		
	If the path is a hyphen (-), path becomes stdin.

	ACCEPTED VAR_NAMEs:
		homeserver, access_token

	- Lines not containing a VALUE_PAIR with an ACCEPTED VAR_NAME are ignored.
	- Lines beginning with equals (=) after removing tab/space indenting are comments.
	- Each VALUE_PAIR must be on its own line ending in a newline.
	- VAR_NAME is every character after tab/space indenting until the first equals (=).
	- VALUE is every character after the first equals (=) until the first newline (\n).
	- VAR_NAME and VALUE are read as raw text with no escaping or special rules.

ENVIRONMENT
	MATRIX__HOMESERVER                    Matrix homeserver url, ex: https://myhomeserver.org

VALUE PRIORITY
	ARGUEMENT value > ACCESS_TOKEN_FILE value > USER_FILE value > ENVIRONMENT value

EXAMPLES
	# User interactive prompts to enter missing information that's required
	matrix-logout

	# Headless request using ARGUEMENTs
	matrix-logout -T <(printf '%s' 'mytoken') 'https://myhomeserver.org'

	# Create a USER_FILE
	>'/path/to/myuser'
	chmod 600 -- '/path/to/myuser'
	cat <<-'EOF' > '/path/to/myuser'
		homeserver=https://myhomeserver.org
		access_token=my token
	EOF

	# Headless request using a USER_FILE
 	matrix-logout -U '/path/to/myuser'
```
