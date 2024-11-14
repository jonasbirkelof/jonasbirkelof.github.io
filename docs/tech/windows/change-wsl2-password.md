---
title: Change WSL2 Password
---

If you have forgotten your WSL2 password, this is how you change it.

1. Open the terminal.
2. Run `wsl -l` to see all distros and find the one you want to reset the password for. For example, we want to reset the password for user `usr001` in the distro `ubuntu-20.04`.

	```
	wsl -l
	```

1. Set default user to root. You must remove all `-`, `.` and `whitespaces` from the distro name.

	```
	ubuntu2004 config --default-user root
	```

1. Open WSL2 and select a new password.

	```
	passwd usr001
	```
	
1. Open the terminal again and set `usr001` as the default user.

	```
	ubuntu2004 config --default-user usr001
	```