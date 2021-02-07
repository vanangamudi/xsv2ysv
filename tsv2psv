#!/usr/bin/env python3

import csv
import sys
import argparse

import logging

FORMATS = {
    'csv': ','
    , 'tsv': '\t'
    , 'psv': '|'
}

parser = argparse.ArgumentParser()

parser.add_argument("-v",
                    "--verbose",
                    help="increase output verbosity",
                    action="store_true"
)

parser.add_argument("-f",
                    "--from_",
                    help="increase output verbosity",
                    choices= FORMATS.keys(),
                    type=str.lower,
)

parser.add_argument("-t",
                    "--to_",
                    help="increase output verbosity",
                    choices= FORMATS.keys(),
                    type=str.lower,
)


parser.add_argument("files",
                    help="list of files",
                    nargs='+',

)

args = parser.parse_args(sys.argv)
print(parser.prog, args)

if not parser.prog.startswith('xsv2ysv'):
    args.from_, args.to_ = parser.prog[:8].lower().split('2')

else:
    assert args.from_ is not None and args.to_ is not None

print(parser.prog, args)


for filepath in args.files[1:]:
    print('processing {}...'.format(filepath))
    try:
        with open(filepath) as xsv_file:
            reader = csv.reader(xsv_file, delimiter=FORMATS[args.from_])

            writer = csv.writer(
                open(
                    filepath.replace(args.from_, args.to_),
                    'w'
                ),
                delimiter=FORMATS[args.to_]
            )

            for row in reader:
                writer.writerow(row)

    except:
        logging.exception(filepath)
