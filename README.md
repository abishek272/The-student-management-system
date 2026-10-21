
import json
import os

FILE_NAME = "students.json"


def load_students():
    if os.path.exists(FILE_NAME):
        with open(FILE_NAME, "r") as file:
            return json.load(file)
    return []


def save_students(students):
    with open(FILE_NAME, "w") as file:
        json.dump(students, file, indent=4)


def add_student(students):
    student_id = input("Enter student ID: ")

    if any(s["id"] == student_id for s in students):
        print("Student ID already exists!")
        return

    name = input("Enter student name: ")
    age = input("Enter student age: ")
    course = input("Enter student course: ")

    students.append({
        "id": student_id,
        "name": name,
        "age": age,
        "course": course
    })

    save_students(students)
    print("Student added successfully!")


def view_students(students):
    if not students:
        print("No student records found.")
        return

    for student in students:
        print("-" * 30)
        print("ID:", student["id"])
        print("Name:", student["name"])
        print("Age:", student["age"])
        print("Course:", student["course"])


def search_student(students):
    student_id = input("Enter student ID to search: ")

    for student in students:
        if student["id"] == student_id:
            print(student)
            return

    print("Student not found.")


def delete_student(students):
    student_id = input("Enter student ID to delete: ")

    for student in students:
        if student["id"] == student_id:
            students.remove(student)
            save_students(students)
            print("Student deleted successfully!")
            return

    print("Student not found.")


def main():
    students = load_students()

    while True:
        print("\n=== Student Management System ===")
        print("1. Add Student")
        print("2. View Students")
        print("3. Search Student")
        print("4. Delete Student")
        print("5. Exit")

        choice = input("Enter your choice: ")

        if choice == "1":
            add_student(students)
        elif choice == "2":
            view_students(students)
        elif choice == "3":
            search_student(students)
        elif choice == "4":
            delete_student(students)
        elif choice == "5":
            print("Thank you for using the system!")
            break
        else:
            print("Invalid choice. Please try again.")


if __name__ == "__main__":
    main()
