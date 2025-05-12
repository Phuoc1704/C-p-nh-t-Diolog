data class Student(
    var id: Int,
    var name: String,
    var email: String
)
fun showStudentDialog(isUpdate: Boolean, student: Student?, onResult: (Student) -> Unit) {
    val dialogView = LayoutInflater.from(context).inflate(R.layout.dialog_student, null)
    val nameInput = dialogView.findViewById<EditText>(R.id.etName)
    val emailInput = dialogView.findViewById<EditText>(R.id.etEmail)

    if (isUpdate && student != null) {
        nameInput.setText(student.name)
        emailInput.setText(student.email)
    }

    AlertDialog.Builder(context)
        .setTitle(if (isUpdate) "Cập nhật sinh viên" else "Thêm sinh viên")
        .setView(dialogView)
        .setPositiveButton("Lưu") { _, _ ->
            val name = nameInput.text.toString()
            val email = emailInput.text.toString()
            onResult(Student(student?.id ?: generateId(), name, email))
            Toast.makeText(context, "Đã lưu sinh viên", Toast.LENGTH_SHORT).show()
        }
        .setNegativeButton("Hủy", null)
        .show()
}
fun confirmDelete(student: Student, onDelete: () -> Unit) {
    AlertDialog.Builder(context)
        .setTitle("Xóa sinh viên")
        .setMessage("Bạn có chắc muốn xóa ${student.name}?")
        .setPositiveButton("Xóa") { _, _ ->
            onDelete()
            Snackbar.make(recyclerView, "Đã xóa sinh viên", Snackbar.LENGTH_SHORT).show()
        }
        .setNegativeButton("Hủy", null)
        .show()
}
