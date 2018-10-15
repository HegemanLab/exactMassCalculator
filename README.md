# exactMassCalculator

An exact mass calculator for molecular formulas which uses an element's most-abundant isotope for the molecules isotopic composition.

## Implementation

Isotope abundance and atomic mass measurements from [IUPAC-CIAWW](https://www.ciaaw.org)'s **Atomic Weights of the Elements: Review 2000**.

Python Decimal objects are used to track and round significant figures properly. See [atomicWeightsDecimal](https://github.com/HegemanLab/atomicWeightsDecimal) for more info.

### Caution

exactFormulaWeightCalculator expects to read formulas with properly named, case-sensitive, element symbols.
  - e.g., Copper should be specified with `Cu`. `CU` will be read as carbon and uranium.

## Useage

**Simple example:**
```
# formulaWeightCalculator takes tabular files (.tsv) as input
# generate example data
echo "formula\tmass\nCH4\t16\nC2H6\t30\nC2H4\t28" > example.tsv
cat example.tsv

# use the --input or -i parameter to specify the input tabular file
# use the --output or -o parameter to specify the output tabular file
python3 formulaWeightCalculator.py -i example.tsv -o results.tsv
cat results.tsv
```

**Extended, real data, example:**
```
# download test data
curl ftp://ftp.plantcyc.org/Pathways/Data_dumps/PMN13_July2018/aracyc_compounds.20180702 > aracyc.tsv

# specify column header for the formula column with the --formula or -f parameter
# if this parameter is not supplied, the first column will be assumed to contain formulas
# in the case of the header is named "Chemical_formula"
python3 formulaWeightCalculator.py -i aracyc.tsv -o results.tsv -f "Chemical_formula"
head results.tsv

# to remove duplicates use the --unique or -u flag
python3 formulaWeightCalculator.py -i aracyc.tsv -o results.tsv -f "Chemical_formula" -u
head results.tsv

# to sort formulas by their weight use the --sort or -s flag
python3 formulaWeightCalculator.py -i aracyc.tsv -o results.tsv -f "Chemical_formula" -u -s
head results.tsv
```
