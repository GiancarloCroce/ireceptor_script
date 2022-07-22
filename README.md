Python script to search TCRs with specific CDR3 sequences in the iReceptor Gateway (https://gateway.ireceptor.org)



# USAGE

```
python3 search_ireceptor.py --cdr3_file cdr3_file.csv --out_folder out_results_folder
```

--cdr3_file: file containing the CDR3 sequences (see ./test.csv for the format)

--out_folder: output folder where the results will be stored. It contains a) a pickle dictionary when all results are stored together b) a csv file for each TCR containig information about where the TCR was observed (e.g. Pubmed number, patient status etc. etc.)



**example usage**

Install the requirements.txt file (a virtual environment is recommended), and then run:

```
python3 search_ireceptor.py --cdr3_file test.csv --out_folder results_test
```

The results will be stored in ./results_test folder. You'll find a .csv file for each TCR that had at least one hit in iReceptor. For example './results/data_TRA_CAVSKGGGNKLTF.csv' contains the results of the analysis for the alpha chain sequence CAVSKGGGNKLTF (i.e. in which studies TCR sequences with CAVSKGGGNKLTF as CDR3 have been observed).

I usually filter out TCRs that have exactly the the same V,J genes as those in cdr3_file.csv, and I keep ONLY ONE sequence for repertore_id (I'm interested in clonotype, i.e. whether a specific TCR sequence has been observed in other patients) 

If available, also dataset for paired TCRs will be generated, but there is relatively few single cell data for TCRs.

**N.B. --same_VJ option**
There is also an option to select only TCR with the same V,J genes as those in cdr3_file.csv [--same_VJ] direcly when running the script ( python3 search_ireceptor.py --cdr3_file test.csv --out_folder results_test --same_VJ) but there may be some format issues:
iReceptor uses IMGT nomenclature so genes format like TRAV-8\*04 are OK, but TRAV08\*04 or TRAV8-2/4-8 are not. Please check the format of the V,J genes in your dataset if using this option.
