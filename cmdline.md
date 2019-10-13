# Commands I've found to be useful.

## Linux

Dump all TCP traffic on port 8000 on any interface. Useful when trying to figure out what interface a program is bound to.

	sudo tcpdump -i any -nn tcp port 8000

