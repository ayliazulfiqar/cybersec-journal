# Day 23 — Port Scanner v3

## Project

**Project Name:** Python Port Scanner v3

**GitHub Repository:** https://github.com/ayliazulfiqar/port-scanner

## Work Completed

Today, I upgraded my Python port scanner to version 3.

The improvements include:

- Added command-line arguments using `argparse`.
- Added target IPv4 address validation.
- Added port-range validation.
- Added configurable connection timeouts.
- Added configurable worker threads.
- Added service banner grabbing.
- Added an option to save scan results to a file.
- Added error handling and tested the command-line help.

## Testing

- Tested the command-line help using `python3 scanner.py --help`.
- Tested valid and invalid port-range input.
- Checked that a missing target produces an argument error.
- Checked that public IP addresses are rejected by the private-IP validation.
- Tested saving scan results to a file in my authorized lab environment.

## What I Learned

I learned how to combine Python sockets, multithreading, command-line arguments, input validation, and file handling in one project. I also practiced managing commits and synchronizing a local Git repository with GitHub.

## Outcome

Port Scanner v3 is complete, with configurable scanning options, basic safety checks, and optional file output.

**Repository:** https://github.com/ayliazulfiqar/port-scanner
