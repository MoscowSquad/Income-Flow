enum class TransactionType {
    INCOME,
    EXPENSE
}

data class Transaction(
    val description: String,
    val amount: Double,
    val type: TransactionType
)

fun calculateBalance(transactions: List<Transaction>): Double {
    return transactions.sumOf {
        if (it.type == TransactionType.INCOME) it.amount else -it.amount
    }
}

// === Test Cases ===

fun testBalanceWithOnlyIncome() {
    val transactions = listOf(
        Transaction("Salary", 5000.0, TransactionType.INCOME),
        Transaction("Bonus", 1500.0, TransactionType.INCOME)
    )
    val balance = calculateBalance(transactions)
    println(" Test: Only Income → Expected: 6500.0, Got: $balance")
}

fun testBalanceWithIncomeAndExpense() {
    val transactions = listOf(
        Transaction("Salary", 5000.0, TransactionType.INCOME),
        Transaction("Rent", 2000.0, TransactionType.EXPENSE),
        Transaction("Food", 500.0, TransactionType.EXPENSE)
    )
    val balance = calculateBalance(transactions)
    println(" Test: Income & Expense → Expected: 2500.0, Got: $balance")
}

fun testBalanceWithNoTransactions() {
    val transactions = emptyList<Transaction>()
    val balance = calculateBalance(transactions)
    println(" Test: No Transactions → Expected: 0.0, Got: $balance")
}

// === CLI Test Menu ===

fun showTestMenu() {
    while (true) {
        println("\n========== Test CLI ==========")
        println("1. Test Balance with Only Income")
        println("2. Test Balance with Income & Expenses")
        println("3. Test Balance with No Transactions")
        println("4. Exit Test CLI")
        print("Choose a test to run: ")

        when (readln()) {
            "1" -> testBalanceWithOnlyIncome()
            "2" -> testBalanceWithIncomeAndExpense()
            "3" -> testBalanceWithNoTransactions()
            "4" -> {
                println("Exiting Test CLI...")
                return
            }
            else -> println(" Invalid option. Try again.")
        }
    }
}

// الدالة الأساسيه
fun main() {
    showTestMenu()
}
