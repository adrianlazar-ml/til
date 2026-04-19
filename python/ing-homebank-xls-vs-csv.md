\# ING HomeBank: prefer XLS export over CSV for parsing



2026-04-19



ING Romania's HomeBank lets you export account statements in three formats: PDF, CSV, and XLS. For programmatic parsing, skip CSV.



The "CSV" is not a tabular CSV. It is the paginated visual statement (same layout as the PDF) dumped to rows, with each transaction spanning 6 to 10 lines and repeated page headers/footers scattered throughout. Parsing requires a custom line-by-line state machine.



The XLS, generated via JasperReports on the backend, gives one row per transaction with the metadata concatenated in a single Detalii tranzactie cell. Parsing becomes pd.read\_excel plus regex on one column.



Bonus: in the HomeBank web UI, check the "Balanta intermediara" checkbox before exporting. You get a fifth column with the running balance after each transaction, which makes reconciliation trivial.



On 18 years of my own transactions, switching from CSV to XLS shrank the parser from a 150-line state machine to 50 lines of straight pandas.



Note the xlrd engine: ING's XLS is the legacy BIFF format, not modern XLSX, so openpyxl will refuse it.



Tags: python, pandas, banking, romania

