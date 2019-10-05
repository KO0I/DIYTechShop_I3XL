# DIYTechShop_I3XL
Diy Tech Shop I3XL, made by XSSink, is an older printer kit.

The following repository contains all the required files to make changes and
repairs to one of these 3D printer kits.

Requires:
* Arduino software to flash the 3D printer
* Optional: Ano (https://github.com/scottdarch/Arturo) Deprecated, but there is a
  workaround: Older Arduino Software included under arduino


The files include:
* STLs to replace any broken parts
* Marlin as last programmed to adjust firmware settings (toolchain is ano, see runme.sh for the
  programming sequence)
* The documentation and an archive link
* My preferred toolchain was to slice and stl file with Slic3r, then use printrun
  (pronterface.py) to run the printer from a host machine, such as a Raspberry
Pi or an old laptop.
