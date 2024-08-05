### Assignment: Hospital Management System

In this assignment, you will design an Entity-Relationship Diagram (ERD) for a Hospital Management System. The purpose of this task is to help you understand and apply the principles of database design, focusing on the identification of entities, their attributes, and the relationships between them. You will create a visual representation of the system’s data model, which will serve as the foundation for a well-structured and efficient database.

Use this wireframe as a reference to ensure that your ERD aligns with the user flows and functionalities depicted.

![Hospital Management](/04%20-%20ERD/Hospital%20Management%20System.md)


**Estimated Time to Completion:** 120 mins

**Level of Complexity:** Medium

**Entities**
1. Patients: *PatientID, FirstName, LastName, DateOfBirth, Address, Phone*
2. Doctors: *DoctorID, FirstName, LastName, Specialty, Phone*
3. Appointments: *AppointmentID, PatientID, DoctorID, AppointmentDate, Reason*
4. Prescriptions: *PrescriptionID, AppointmentID, Medication, Dosage, Instructions*


**Learning Objectives**
- Learn to identify and define entities and their attributes in a healthcare context.
- Understand the relationships between patients, doctors, appointments, and prescriptions.
- Gain experience in modeling one-to-many relationships and ensuring data integrity.
- Develop the ability to create ERDs that reflect the workflows and requirements of a hospital management system.

---

**Relationships**
- A patient can have multiple appointments with different doctors.
- A doctor can see multiple patients in different appointments.
- An appointment can result in multiple prescriptions.

**Tasks**
1. Design the ERD for the Hospital Management System.
2. Identify primary keys, foreign keys, and relationships between the entities.
3. Ensure data integrity by defining appropriate constraints and rules.