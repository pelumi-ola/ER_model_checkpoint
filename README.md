## Here is the Entity-Relationship (ER) Model corresponding to the gym management system.

# Entity-Relationship Model (ERM)

## Entities and Attributes

### GYMNASIUM

Primary Key: `Gym_ID`

Attributes:

- Gym_ID (PK)
- Name
- Address
- Telephone

Relationship:

- One gymnasium registers many members
- One gymnasium organizes many sessions

Cardinality:

GYMNASIUM (1) ─────── (N) MEMBER
GYMNASIUM (1) ─────── (N) SESSION

### MEMBER

Primary Key: `Member_ID`

Attributes:

- Member_ID (PK)
- Last_Name
- First_Name
- Address
- Date_of_Birth
- Gender
- Gym_ID (FK)

Relationship:

- A member registers in exactly one gymnasium
- A member can register for many sessions

### SESSION

Primary Key: `Session_ID`

Attributes:

- Session_ID (PK)
- Sport_Type
- Schedule
- Max_Capacity (fixed = 20)
- Gym_ID (FK)

Relationships:

- A session belongs to one gymnasium
- A session has many members (max 20)
- A session is led by up to 2 coaches

### COACH

Primary Key: `Coach_ID`

Attributes:

- Coach_ID (PK)
- Last_Name
- First_Name
- Age
- Specialty

Relationship:

- A coach can lead multiple sessions
- A session can have up to 2 coaches

## Associative Entities (For Many-to-Many Relationships)

### REGISTRATION

(Resolves MEMBER–SESSION Many-to-Many)

- Primary Key: Registration_ID
- Foreign Keys: Member_ID, Session_ID

Attributes:

- Registration_ID (PK)
- Member_ID (FK)
- Session_ID (FK)
- Registration_Date

Cardinality:

MEMBER (1) ─────── (N) REGISTRATION (N) ─────── (1) SESSION

Constraint:

A session can have maximum 20 registrations.

### SESSION_COACH

(Resolves SESSION–COACH Many-to-Many)

Composite Primary Key: (Session_ID, Coach_ID)

Attributes:

- Session_ID (FK)
- Coach_ID (FK)

Cardinality:

SESSION (1) ─────── (N) SESSION_COACH (N) ─────── (1) COACH

Constraint:

Maximum 2 coaches per session.

# Complete ER Structure (Text Diagram)

GYMNASIUM

Gym_ID (PK)
Name
Address
Telephone

        1
        |
        | registers
        |
        N

MEMBER

Member_ID (PK)
Last_Name
First_Name
Address
Date_of_Birth
Gender
Gym_ID (FK)

        1
        |
        | has
        |
        N

SESSION

Session_ID (PK)
Sport_Type
Schedule
Max_Capacity
Gym_ID (FK)

MEMBER (N) ────< REGISTRATION >──── (N) SESSION

SESSION (N) ────< SESSION_COACH >──── (N) COACH

COACH

- Coach_ID (PK)
- Last_Name
- First_Name
- Age
- Specialty

# Cardinality Summary

| Relationship        | Type                              |
| ------------------- | --------------------------------- |
| Gymnasium – Member  | 1 : N                             |
| Gymnasium – Session | 1 : N                             |
| Member – Session    | N : N (via Registration)          |
| Session – Coach     | N : N (max 2 coaches per session) |

---

# Business Rules Included

1. Each member registers in exactly one gymnasium.
2. Each session belongs to one gymnasium.
3. A session can have maximum 20 members.
4. A session can be led by maximum 2 coaches.
5. A coach can lead multiple sessions.
