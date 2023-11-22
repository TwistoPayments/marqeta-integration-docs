# Clearing files

In addition to webhooks marqeta also provides us with Mastercard clearing files through SFTP.
We download these files and crosscheck with our database if we have these records in `MarqetaProcessClearingFileTask`.

## File structure

File is an CSV file with columns described in tasks `fieldnames` attribute. For detailed info about the fields see
[Replacement](./Mastercard_fields.pdf)
We use only records with MTI 1240 which are messages we are interested in.
Based on a service type we determine whether the transaction was regular clearing or refund (when it starts '20')

## Task behaviour

The task `MarqetaProcessClearingFileTask` is run every night. It connects to Marqeta's sftp server and looks for not
processed files (based on their name and our record in `MarqetaClearingFileProcessingLog`)

Tasks tries to pair clearings using network_reference_id value from file and transaction data. If no match is found, we
try to find related clearing based on amount, merchant and card number.

If no clearing is found a `MarqetaUnmappedClearing` record is created.
