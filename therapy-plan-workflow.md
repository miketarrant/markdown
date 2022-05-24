graph
classDef mdclass fill:#fA1;
classDef cadeclass fill:#3ff; 

Provider[[Ordering Provider fa:fa-user-md]]
Provider:::mdclass --> A(fa:fa-user-md Logs in to home clinic DEP)
A:::mdclass --> B(fa:fa-user-md Opens patient chart)
B:::mdclass --> C(fa:fa-user-md Selects appropriate therapy plan)
C:::mdclass --> D(fa:fa-user-md Enters Start Date in Proprities)
D:::mdclass --> E(fa:fa-user-md Enters Treatment DEP in Properities)
E:::mdclass --> F(fa:fa-user-md Modifies orders and intervals)
F:::mdclass --> G(fa:fa-user-md Signs therapy plan orders)
G:::mdclass --> End(fa:fa-user-md Ordering complete)
End:::mdclass

Cadence[[Clinic Scheduler fa:fa-user-clock]]
G --> |Scheduling request is generated|1
E -.- |Treatment DEP context|1
D -.- |Start date context|1
1 --> 2(fa:fa-user-clock Scheduler examines request details)
2:::cadeclass --> 3(fa:fa-user-clock Contacts patient to determine availability)
3:::cadeclass --> 4(fa:fa-user-clock Schedules visits)
4:::cadeclass --> 5(fa:fa-user-clock Scheduler updates Start Date in therapy plan)
5:::cadeclass
Cadence:::cadeclass ---> 1{{Request appears in scheduling workqueue}}


FACT[[Financial Clearance Team fa:fa-user-check]]
FACT ---> H{{Request appears in referral workqueue}}
A -.- |Clinic DEP context|H
F -.- |Infusion med context|H
G --> |Referral is generated|H
H --> I(Prior auth magic is worked)
I --> J(Referral is approved)

Nurse[Registered Nurse fa:fa-user-nurse]




