# Ultimate Hosts Blacklist whitelisting script

This branch will help you clean your list or host file with the whitelist list which is used by the [Ultimate Hosts Blacklist](https://github.com/mitchellkrogza/Ultimate.Hosts.Blacklist) infrastructure.

## Requirements

If you want to use the script, please take the time to clone this branch and install the requirements with:

    pip3 install --user -r requirements.txt

## Complementary whitelist

Our script allow us to link a file to the system which will be used in complementary of our whitelist list.

### `ALL ` as special marker

If you already used a whitelist list you already know that we generaly only list all domains we want to whitelist one by one.

 It's also possible to do that with our whitelisting system but we can do more.
Indeed we also can use the `ALL ` which will tell the system to regex check againt what follows.

### Understanding what we actually do

If we have the following secondary whitelist list:

```
facebook.com
ALL .gov
```

our system actually create a one line regular expression which will be checked against every line. At the end on the system side for the given whitelist list we generate the following regular expression.

```re
^facebook\.com$|^www\.facebook\.com|\.gov$
```

Which actually means that we whitelist:

* `facebook.com` and `www.facebook.com`
* all domains which ends with `.gov`

### INVALID characters

#### When the `ALL ` marker is used

* `$`
    * As we automatically append `$` to the end, you should not use this character.

* `\`
    * As we automatically escape the given expression, you should not explicitly escape your regular expression when declaring an `ALL ` marker.

## Usage of the script

    usage: whitelisting.py [-h] [-f FILE] [-w WHITELIST] [-o OUTPUT]

    The tool to whitelist a list or a hosts file with the Ultimate Hosts Blacklist
    infrastructure.

    optional arguments:
    -h, --help            show this help message and exit
    -f FILE, --file FILE  Read the given file and remove all element to
                            whitelist.
    -w WHITELIST, --whitelist WHITELIST
                            Read the given file and append its data to the our
                            whitelist list.
    -o OUTPUT, --output OUTPUT
                            Save the result to the given filename or path.

    Crafted with ♥ by Nissar Chababy (Funilrys)

