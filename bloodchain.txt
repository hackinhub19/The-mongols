blockchain for blood donation

initial blockchain for getting the details and creation

"
package com.moro.blockchain;

import java.util.Arrays;

public class BlockChainExample {

    public static void main(String[] args) {

        /*
        BlockChain 
        Block - Hash of Previous Block + Transactions
        Chained together.
         */

        Transaction transaction1 = new Transaction("Peter", "Sam", 10 pints);
        Transaction transaction2 = new Transaction("Sam", "Ryan", 10 pints);
        Transaction transaction3 = new Transaction("Sam", "Ryan", 10 pints);
        Transaction transaction4 = new Transaction("Ryan", "Peter",10 pints);

        Block firstBlock = new Block(0, Arrays.asList(transaction1, transaction2));
        System.out.println(firstBlock.hashCode());
        Block secondBlock = new Block(firstBlock.hashCode(), Arrays.asList(transaction3));
        System.out.println(secondBlock.hashCode());
        Block thirdBlock = new Block(secondBlock.hashCode(), Arrays.asList(transaction4));
        System.out.println(thirdBlock.hashCode());

    }
}"

seperate class for block
"
package com.moro.blockchain;

import java.util.List;

public class Block {


    private int previousHash;
    private List<Transaction> transactions;

    public Block(int previousHash, List<Transaction> transactions) {
        this.previousHash = previousHash;
        this.transactions = transactions;
    }

    public int getPreviousHash() {
        return previousHash;
    }

    public void setPreviousHash(int previousHash) {
        this.previousHash = previousHash;
    }

    public List<Transaction> getTransactions() {
        return transactions;
    }

    public void setTransactions(List<Transaction> transactions) {
        this.transactions = transactions;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Block block = (Block) o;

        if (previousHash != block.previousHash) return false;
        return transactions != null ? transactions.equals(block.transactions) : block.transactions == null;
    }

    @Override
    public int hashCode() {
        int result = previousHash;
        result = 31 * result + (transactions != null ? transactions.hashCode() : 0);
        return result;
    }
}"

again a seperate class for transaction
"
package com.moro.blockchain;

public class Transaction {

    private String sourceName;
    private String destinationName;
    private Long sum;

    public String getSourceName() {
        return sourceName;
    }

    public void setSourceName(String sourceName) {
        this.sourceName = sourceName;
    }

    public String getDestinationName() {
        return destinationName;
    }

    public void setDestinationName(String destinationName) {
        this.destinationName = destinationName;
    }

    public Long getSum() {
        return sum;
    }

    public void setSum(Long sum) {
        this.sum = sum;
    }

    public Transaction(String sourceName, String destinationName, Long sum) {
        this.sourceName = sourceName;
        this.destinationName = destinationName;
        this.sum = sum;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;

        Transaction that = (Transaction) o;

        if (sourceName != null ? !sourceName.equals(that.sourceName) : that.sourceName != null) return false;
        if (destinationName != null ? !destinationName.equals(that.destinationName) : that.destinationName != null)
            return false;
        return sum != null ? sum.equals(that.sum) : that.sum == null;
    }

    @Override
    public int hashCode() {
        int result = sourceName != null ? sourceName.hashCode() : 0;
        result = 31 * result + (destinationName != null ? destinationName.hashCode() : 0);
        result = 31 * result + (sum != null ? sum.hashCode() : 0);
        return result;
    }
}"