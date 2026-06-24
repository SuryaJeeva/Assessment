1.)Job Scheduling Problem using Backtracking and Constraint Satisfaction Techniques.


# Job Scheduling using Backtracking

jobs = [
    {"id": "J2", "duration": 1, "deadline": 3},
    {"id": "J1", "duration": 2, "deadline": 4},
    {"id": "J3", "duration": 2, "deadline": 5}
]

employees = ["E1", "E2", "E3"]

# Employees qualified for each job
qualified = {
    "J1": ["E1", "E2"],
    "J2": ["E1", "E3"],
    "J3": ["E2", "E3"]
}

assignment = {}
employee_time = {emp: 0 for emp in employees}

def is_valid(job, employee):
    """Check if assigning a job to an employee satisfies constraints."""
    completion_time = employee_time[employee] + job["duration"]
    return completion_time <= job["deadline"]

def backtrack(job_index):
    """Recursively assign jobs using backtracking."""
    if job_index == len(jobs):
        return True  # All jobs assigned

    job = jobs[job_index]

    for emp in qualified[job["id"]]:
        if is_valid(job, emp):

            # Assign job
            assignment[job["id"]] = emp
            employee_time[emp] += job["duration"]

            # Recur for next job
            if backtrack(job_index + 1):
                return True

            # Backtrack
            employee_time[emp] -= job["duration"]
            del assignment[job["id"]]

    return False

# Run scheduling
if backtrack(0):
    print("Feasible Schedule Found:\n")
    for job, emp in assignment.items():

    OUTPUT:
    Feasible Schedule Found:

J1 --> E1
J2 --> E3
J3 --> E2




2.)Exam Timetabling using Graph Coloring and Backtracking:


# Exam Timetabling using Graph Coloring (Backtracking)

# Conflict graph
graph = {
    'Math': ['Physics', 'Chemistry'],
    'Physics': ['Math', 'English'],
    'Chemistry': ['Math'],
    'English': ['Physics']
}

# Available time slots
time_slots = ["Slot1", "Slot2", "Slot3"]

schedule = {}

def is_safe(exam, slot):
    for neighbor in graph[exam]:
        if neighbor in schedule and schedule[neighbor] == slot:
            return False
    return True

def graph_coloring(exams, index):
    if index == len(exams):
        return True

    exam = exams[index]

    for slot in time_slots:
        if is_safe(exam, slot):
            schedule[exam] = slot

            if graph_coloring(exams, index + 1):
                return True

            del schedule[exam]  # Backtrack

    return False

exams = list(graph.keys())

if graph_coloring(exams, 0):
    print("Exam Schedule:")
    for exam, slot in schedule.items():
        print(f"{exam} -> {slot}")
else:
    print("No valid schedule exists.")


    OUTPUT:
    Exam Schedule:
Math -> Slot1
Physics -> Slot2
Chemistry -> Slot2
English -> Slot1

        print(f"{job} --> {emp}")
else:
    print("No feasible schedule exists.")
