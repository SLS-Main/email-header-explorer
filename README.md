# TraceMail Email Header Explorer

TraceMail is a browser-based email header analyzer that turns raw message
headers into an approachable delivery and security report. It is designed to
give beginners plain-language explanations while preserving the evidence and
technical detail needed by administrators and security analysts.

All parsing happens locally in the browser. Pasted headers are not uploaded or
sent to an external service.

## Features

- Parses folded and repeated RFC-style header fields.
- Summarizes SPF, DKIM, DMARC, and ARC authentication results.
- Reconstructs `Received` headers into a chronological delivery route.
- Opens each route hop in a detailed investigation dialog.
- Identifies transport encryption, ciphers, server providers, IP address types,
  timestamps, and delays between hops.
- Groups fields into identity, authentication, routing, message, content,
  security, vendor diagnostic, and other categories.
- Shows the real header field name alongside a beginner-friendly description.
- Provides searchable, expandable, syntax-highlighted raw evidence.
- Supports desktop and mobile layouts without a build step.

## Requirements

- Python 3, used only to serve the static files locally
- A modern web browser
- Node.js and npm for the optional JavaScript syntax check

## Run Locally

```sh
npm start
```

Open `http://localhost:4173` in a browser. If viewing from another device on the
same network, use the host machine's IP address with port `4173`.

Paste the complete raw message header into the editor and select **Analyze
header**.

## Validation

Check the application JavaScript for syntax errors:

```sh
npm run check
```

## Privacy

Email headers can contain names, addresses, internal hostnames, IP addresses,
message identifiers, and security infrastructure details. Treat them as
sensitive data.

The local `header-example.txt` file is intentionally excluded through
`.gitignore` because it contains a real email header. Do not remove that ignore
rule or commit real headers to the repository. Use sanitized test data for any
future public examples.

## Project Structure

```text
index.html    Application structure and report interface
styles.css    Responsive design, editor, route, and dialog styling
app.js        Header parser, analysis logic, and UI interactions
package.json  Local server and validation commands
```

## Technical Notes

TraceMail is a dependency-free static application. Provider identification and
IP classification are informational heuristics based on header contents; they
do not perform DNS, geolocation, reputation, or live authentication lookups.
Results should be reviewed alongside the original message and mail-system logs
when making security decisions.
