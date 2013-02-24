# Usage #

First, download your transactions from your Mint account. You can find the export link
on the [transactions page](https://wwws.mint.com/transaction.event), in very small type
at the bottom right, or by searching the page for "Export all".

Then run the script, like so:

    mint-to-ledger [-h] csv_file ledger_file

# Known Issues #

There are a couple of problems with the resulting ledger due to incomplete information on
Mint's part. In other words, they may or may not ever be fixed.

## Transfers between accounts ## 

Mint represents a transfer between two of your own accounts by assigning the category 
"Transfer" to the transaction appearing on each account statement. The script interprets
this as one transaction from the source account to "Expenses:Transfer" and another from 
"Income:Transfer" to the destination account. It should really be expressed as a single
transaction from one Assets account to the other.

I've special-cased this for cash withdrawals since Mint provides the category "Transfer
for Cash Spending", but haven't dealt with the transfers to and from accounts with 
arbitrary names. It seems possible to allow for user-defined categories which are
interpreted as transfers rather than expenses, but I haven't tried to implement this yet.

## Non-transactional balance changes ##

If an account ever changes in value due to something other than a transaction (for 
example, market movements affect the balance of your brokerage account), Mint fetches the
correct balance but doesn't indicate it in the transactions file. I doubt I can ever fix
this since the relevant information just isn't provided.
