# Python-Apple-EFI-Patcher
patcher.py is a python3 script designed to automate the patching process of Apple EFI Rom dumps. The script can change the serial number, which will also automatically change the hwc field, and correct the CRC32 for the Fsys block. The script also has the ability to remove firmware locks / clear NVRAM and to Clear ME Regions. Currently, the ME Region patching process in patcher.py works correctly, but the supplied ME Regions are mostly untested. Although, those that have been tested thus far all work correctly. Alterantively, you can substitute your own ME Region files if desired.

# Usage:
Place patcher.py, offsets.py, database.json and the ME_Regions folder into the same directory. Run as follows:

`python3 patcher.py -i <input_efi_filename> -o <output_efi_filename> -t <efi_type_#> -s <serial_to_insert> -m <me_region_filename> -r`

__example:__ `python3 patcher.py -i firmware.bin.bin -o dump.bin -t 5 -s ABCDEFGH1234 -m ME_Regions/MBA61/10.13.6_MBA61_0107_B00.rgn -r`

__Note:__ You can drag and drop files into the terminal to avoid having to type locations.

__Options:__
* -i <input_efi_filename>     -- name of the file to be modified</li>
* -o <output_efi_filename>    -- name of the newly modified file</li>
* -t <efi_type>               -- type # of efi (see list below)</li>
* -s <serial_to_insert>       -- serial number to be inserted</li>
* -m <me_region_filename>     -- name of the ME Region file to insert</li>
* -r                          -- remove firmware lock</li>

__EFI Type Options:__

1. EFI Type 1
   - 2008 A1278 820-2327

2. EFI Type 2
   - 2011 A1278 820-2936
   - 2011 A1286 820-2915

3. EFI Type 3
   - 2011 A1369 820-3023

4. EFI Type 4 
   - 2012 A1278 820-3115
   - 2012 A1286 820-3330
   - late 2012 / early 2013 A1398 820-3332
   - late 2012 / early 2013 A1425 820-3462
   - 2012 A1465 820-3208
   - 2012 A1466 820-3209

5. EFI Type 5
   - 2013/2014 A1502 820-3476
   - 2013/2014 A1398 820-3662
   - 2013/2014 A1398 820-3787
   - 2013/2014 A1465 820-3435
   - 2013/2014 A1466 820-3437

6. EFI Type 6
   - 2015 A1398 820-00138
   - 2015 A1465 820-00164
   - 2015-2017 A1466 820-00165
   - 2015 A1502 820-4924

7. EFI Type 7
   - 2017 A1706 820-00239
   - 2017 A1707 820-00928

__Note:__ ME Regions are mostly untested! They require more real world testing. Feedback would be appreciated.
ME Regions have been extracted from macOS 10.12.6, 10.13.6, 10.14.6 and 10.15.b8. They are contained in the ME_Regions folder. Each subfolder corresponds to a system type. (example: MBA61 = MacBook Air 6,1). Each ME region file is named in accordance to the macOS version from which it was extracted, the system type, the Boot Rom Version and the ME Version. (example: 10.13.6_MBA61_0107_B00_9.5.3.1526.rgn, means that the ME Region was extracted from macOS High Sierra 10.13.6, it is for a MacBook Air 6,1, it came from an EFI with Boot Rom Version 0107_B00 and the ME Version is 9.5.3.1526). In some instances, regions between macOS versions may be identical. It seemed that anything extracted from .scap files rather an .fd files were the same between OS versions. You can use something like <a href="https://ridiculousfish.com/hexfiend/">hex fiend</a> to compare and see if they are identical, or <a href="https://github.com/platomav/MEAnalyzer">ME Analyzer</a> to find out the ME Version. Also, anything extracted from macOS 10.14.6 onward has no references to Boot Rom Versions in their names. Not that it particularly matters, what you want to match up is the ME version number.

__Update:__ ME Regions 10.14.6_MBP91_8.0.4.1441.rgn and 10.14.6_MBA71_10.0.35.1012.rgn have been tested and verified working. This would stand to reason that the other extracted regions should also work as expected!

Offsets for new types of EFI's can also be easily added. Just follow the format provided in the offsets.py file and append your additions. Use something like <a href="https://ridiculousfish.com/hexfiend/">hex fiend</a> to acquire the line position offsets for each region.
