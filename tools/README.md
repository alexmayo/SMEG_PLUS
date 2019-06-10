# Useful Tools

I've compiled a list of useful tools that come in handy when modifying the firmware, especially when applying updated via USB on newer SMEG+ IV2 units.

### Contents
- [crc.cpp](#crc_cpp)  


---

<a name="crc_cpp"/>
##### crc.cpp
This is a custom tool to compile crc for firmware files.
The original version of this C++ code is by sven337 over at the Planete Citroen forums ([see here](http://www.planete-citroen.com/forum/showthread.php?152326-Ing%C3%A9nierie-inverse-du-RT6)).

__Instructions__
- Once the `.bin` has been recompiled,  simply run `./crc FILENAME.bin` to generate the last 4 characters of the CRC. Place these four characters into the first line of the `.inf` file.
- Once the `.inf` file has been edited with the new characters, run `./crc FILENAME.bin.inf` to generate the first four characters of the CRC.

__Example__
- Initial CRC in `upgrade_lib.out.inf` file. Currently, if we make any changes to the `.out` file, then the edited file will not pass the CRC checks. To fix this, we need to update the .inf file with the new checksum result.
    > 219b7a18

- Make the desired changes to `upgrade_lib.out`.

- Generate the 2nd part of the CRC using...
    ```
    $ ./crc upgrade_lib.out
    Computed FILE CRC ****5a08
    ```

- Now we change the `.inf` to include the new 2nd part of the CRC.
    > 219b5a08

- Generate the 1st part of the CRC using...
    ```
    $ ./crc upgrade_lib.out.inf
    Computed INF CRC as 204a****
    ```

- Now we change the `.inf` to include the new 1st part of the CRC.
    > 204a5a08

- The file will now pass the CRC check.
