# Student_Management
Student Project
while True:
    print("\nStudent Record Management")
    print("1. Add Student")
    print("2. View Student")
    print("3. Search Student")
    print("4. Update Marks")
    print("5. Percentage")
    print("6. Exit")

    ch = input("Enter choice: ")

    if ch == "1":
        student = input("Enter student name: ")
        subjects = ["Maths", "Science", "SST", "Hindi"]
        marks_list = []

        found = False

        try:
            with open("student.txt", "r") as f:
                for line in f:
                    data = line.strip().split(",")
                    if student == data[0]:
                        found = True
                        break
        except FileNotFoundError:
            pass

        if found:
            print("Student already exists")
        else:
            for sub in subjects:
                m = float(input(f"Enter marks in {sub}: "))
                marks_list.append(str(m))

            with open("student.txt", "a") as f:
                line = student + "," + ",".join(marks_list) + "\n"
                f.write(line)

            print("Marks added successfully")

    elif ch == "2":
        student = input("Enter student name to view: ")
        found = False

        try:
            with open("student.txt", "r") as f:
                for line in f:
                    data = line.strip().split(",")
                    if student == data[0]:
                        print("Student:", data[0])
                        print("Marks:", data[1:])
                        found = True
                        break

            if not found:
                print("Student not found")

        except FileNotFoundError:
            print("No records found")

    elif ch == "3":
        student = input("Enter student name to search: ")
        found = False

        try:
            with open("student.txt", "r") as f:
                for line in f:
                    data = line.strip().split(",")
                    if student == data[0]:
                        print("Student found")
                        found = True
                        break

            if not found:
                print("Student not found")

        except FileNotFoundError:
            print("No records found")

    elif ch == "4":
        student = input("Enter student name: ")

        try:
            with open("student.txt", "r") as f:
                lines = f.readlines()

            found = False

            with open("student.txt", "w") as f:
                for line in lines:
                    data = line.strip().split(",")

                    if student == data[0]:
                        found = True
                        marks = []

                        for sub in ["Maths", "Science", "SST", "Hindi"]:
                            m = input(f"Enter new marks in {sub}: ")
                            marks.append(m)

                        f.write(student + "," + ",".join(marks) + "\n")
                        print("Marks updated")
                    else:
                        f.write(line)

            if not found:
                print("Student not found")

        except FileNotFoundError:
            print("No records found")

    elif ch == "5":
        student = input("Enter student name: ")
        found = False

        try:
            with open("student.txt", "r") as f:
                for line in f:
                    data = line.strip().split(",")

                    if student == data[0]:
                        marks = list(map(float, data[1:]))
                        total = sum(marks)
                        percent = total / 400 * 100

                        print("Student:", student)
                        print("Total Marks:", total)
                        print("Percentage:", round(percent, 2), "%")

                        found = True
                        break

            if not found:
                print("Student not found")

        except FileNotFoundError:
            print("No records found")

    elif ch == "6":
        print("Program closed")
        break

    else:
        print("Invalid choice")
