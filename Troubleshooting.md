# Assertion 'res >= 4' failed
### Error
During the first time you will try to upload a script to Digispark, you will probably encounter this error:
```diff
- micronucleus: library/micronucleus_lib.c:66: micronucleus_connect: Assertion `res >= 4' failed.
- Aborted (core dumped)
```
### Solution  
This error is caused because the Arduino IDE doesn't have permission to access the digispark controller. Solution: 
- Create a file named /etc/udev/rules.d/digispark.rules  
- Add the following line to the file: ```SUBSYSTEM=="usb", ATTR{idVendor}=="16d0", ATTR{idProduct}=="0753", MODE="0660", GROUP="dialout"```
- This will cause the digispark to show up with mode ```0660 (-rw-rw----)``` and owned by group ```dialout```, which is consistent with how other usb-serial devices show up.  Optionally, you can change the group or the mode if you'd like.  (E.g. ```MODE="0666"``` will be writable by any user on the system.)
- [Source](https://digistump.com/board/index.php?topic=106.0)
