# gnssparser
Data parser for raw binary files from GNSS receiver.  This is currently under
active development and only has basic functionality.  Presently, the software
can handle raw data files from Novatel and Septenrio GNSS receivers and will
read high-rate (50-100 Hz) measurements of phase and power.


## Installation

This package is pip installable from github.

```
pip install git+https://github.com/Polar-Cap-Scintillation/gnssparser.git
```

To install locally for development, first clone the repository, then install.

```
git clone https://github.com/Polar-Cap-Scintillation/gnssparser.git
cd gnssparser
pip install -e .
```


## Usage

A basic example of how to read data from both a novatel and septentrio datafile
is shown below.

```
from gnssparser import parse_novatel, parse_septentrio

# Read novatel file
filename = 'novatel_file.nvd.gz'
wnc, tow, phase, power = parse_novatel.read_file(filename)

# Read septentrio file
filename = 'septentrio_file_.gz'
wnc, tow, phase, power = parse_septentrio.read_file(filename)
```

The returned values for both functions are the GPS time stamps week number
(`wnc`) and time of week in seconds (`tow`), both of which are 1D arrays. The
returned phase and power are both nested dictionaries, where the first key is
the PRN (as an `int`) and the second is the name of the signal frequency, i.e.
`GPS_L1-CA`.  Note that novatel receivers only measure the `L1` signal.


