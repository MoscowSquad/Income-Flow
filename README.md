 package org.kotlin.unlimited

// عرض الرصيد بعد التحديث
// ورجوع المستخدم للـ Main Menu

// 1. نوع المعاملة
enum class TransactionType {
    INCOME, // الدخل
    EXPENSE // المصروف
}

// 2. تعريف المعاملة
data class Transaction(
    val description: String, // وصف المعاملة
    val amount: Double,      // المبلغ
    val type: TransactionType // نوع المعاملة
)

// دالة حساب الرصيد بعد أى عملية إيداع أو صرف
fun showBalanceAfterUpdate(transactions: List<Transaction>) {  //بتاخد ليستة المعلومات ك input
    val balance = transactions.sumOf { transaction ->
        if (transaction.type == TransactionType.INCOME) {
            transaction.amount
        } else {
            -transaction.amount
        }
    }

    println("\nCurrent balance after update: $balance EGP\n")
    println("Press Enter to return to the main menu...")
    readln()
    showMainMenu()  //هنا بترجع اليوزر للمنيو الرئيسى
}

// 4. دالة القائمة الرئيسية
fun showMainMenu() {
    println(" Main Menu ")
    println("1. Add Income")
    println("2. Add Expense")
    println("3. Show Balance")
    println("4. Exit")
}

// 5. الدالة الرئيسية
fun main() {
    val transactions = listOf(
        Transaction("Salary", 5000.0, TransactionType.INCOME),
        Transaction("Freelance", 2000.0, TransactionType.INCOME),
        Transaction("Rent", 1200.0, TransactionType.EXPENSE),
        Transaction("Food", 800.0, TransactionType.EXPENSE)
    )

    showBalanceAfterUpdate(transactions) // استدعاء الدالة عشان تعرض الرصيد
}
