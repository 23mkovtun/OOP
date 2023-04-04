class Student:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.finished_courses = []
        self.courses_in_progress = []
        self.grades = {}

    def rate_hw(self, lecturer, course, grade):
        if isinstance(lecturer, Lecturer) and course in self.courses_in_progress and course in lecturer.courses_attached:
            if course in lecturer.grades:
                lecturer.grades[course] += [grade]
            else:
                lecturer.grades[course] = [grade]
        else:
            return 'Ошибка'
        
class Mentor:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.courses_attached = []
        
        
class Lecturer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.grades = {}

class Reviewer(Mentor):
    def __init__(self, name, surname):
      super().__init__(name, surname)
    
    def rate_hw(self, student, course, grade):
        if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
            if course in student.grades:
                student.grades[course] += [grade]
            else:
                student.grades[course] = [grade]
        else:
            return 'Ошибка'
        
# лекторы
best_lecturer_1 = Lecturer('Alex', 'Yurin')
best_lecturer_1.courses_attached += ['Python']

best_lecturer_2 = Lecturer('Tutti', 'Frutti')
best_lecturer_2.courses_attached += ['C++']

best_lecturer_3 = Lecturer('Lisa', 'Grady')
best_lecturer_3.courses_attached += ['Python']

# проверяющие
cool_reviewer_1 = Reviewer('Olga', 'Molga')
cool_reviewer_1.courses_attached += ['Python']
cool_reviewer_1.courses_attached += ['C++']

cool_reviewer_2 = Reviewer('Ted', 'Baker')
cool_reviewer_2.courses_attached += ['Python']
cool_reviewer_2.courses_attached += ['C++']

# студенты 
student_1 = Student('Igor', 'Romanov')
student_1.courses_in_progress += ['Python', 'C++']
student_1.finished_courses += ['Java']

student_2 = Student('Mark', 'Kovtun')
student_2.courses_in_progress += ['C++']
student_2.finished_courses += ['Введение в программирование']

student_3 = Student('Bella', 'Ivanova')
student_3.courses_in_progress += ['Python']
student_3.finished_courses += ['Введение в программирование']

# оценки лекторам
student_1.rate_hw(best_lecturer_1, 'Python', 9)
student_1.rate_hw(best_lecturer_1, 'Python', 9)
student_1.rate_hw(best_lecturer_1, 'Python', 9)

student_2.rate_hw(best_lecturer_2, 'C++', 4)
student_2.rate_hw(best_lecturer_2, 'C++', 7)
student_2.rate_hw(best_lecturer_2, 'C++', 7)

student_3.rate_hw(best_lecturer_3, 'Python', 5)
student_3.rate_hw(best_lecturer_3, 'Python', 6)
student_3.rate_hw(best_lecturer_3, 'Python', 7)

# оценки студентам 
cool_reviewer_1.rate_hw(student_1, 'Python', 8)
cool_reviewer_1.rate_hw(student_1, 'Python', 9)
cool_reviewer_1.rate_hw(student_1, 'Python', 7)

cool_reviewer_2.rate_hw(student_2, 'C++', 8)
cool_reviewer_2.rate_hw(student_2, 'C++', 10)
cool_reviewer_2.rate_hw(student_2, 'C++', 9)

cool_reviewer_2.rate_hw(student_3, 'Python', 8)
cool_reviewer_2.rate_hw(student_3, 'Python', 7)
cool_reviewer_2.rate_hw(student_3, 'Python', 3)
cool_reviewer_2.rate_hw(student_3, 'Python', 8)


print(student_1.grades)
print(best_lecturer_1.grades)
