# SmartMove Transport Solutions (Lite)

The trimmed group project: Oracle (schema, PL/SQL, reports), MongoDB (two collections) and a
5-screen web app. Every table has 10 sample rows or fewer.

## What is in it

| Requirement | Where |
|---|---|
| ER / EER diagram | `diagrams/SmartMove_ER_EER_Diagrams.pdf` |
| Oracle schema (vehicle, driver, route, passenger, trip scheduling, booking, payment, maintenance, feedback) | `database/01_schema.sql` |
| Sample data (10 rows or fewer per table) | `database/02_sample_data.sql` |
| 4 triggers | `database/03_triggers.sql` |
| Package `smartmove_pkg`: 2 functions, 4 procedures, ref-cursor functions, report procedures, named exceptions | `database/04_smartmove_pkg.sql` |
| 5 business reports | `smartmove_pkg.rpt_*` (demo in `database/05_demo.sql`) and the Reports screen |
| MongoDB: `gps_tracking`, `feedback_media` | `mongodb/` |
| Web app: Dashboard, Trips and booking, Bookings and payment, Reports, plus GPS tracking and Feedback (MongoDB) | `backend/` + `frontend/` |

## Run order

**1. Oracle** (FreeSQL or local). Run each file as a whole script, one at a time, in this order:
`01_schema.sql` > `02_sample_data.sql` > `03_triggers.sql` > `04_smartmove_pkg.sql` > `05_demo.sql`.
Always rerun 01 first if you rerun 02 (01 wipes everything and resets the sequences).
No `SET` or `PROMPT` lines are used, so the files run unchanged on FreeSQL and in SQL Developer.

**2. Backend**
```
cd backend
npm install
copy .env.example .env      then put your Oracle (and MongoDB) details in .env
npm run check
npm run dev
```

**3. MongoDB** (optional, once per cluster)
```
cd mongodb
npm install
npm run setup
npm run seed
```

**4. Frontend** (second terminal)
```
cd frontend
npm install
npm run dev                 open http://localhost:5173
```

## Four-minute demo

1. **Trips and booking**: open a scheduled trip (for example R01 tomorrow), choose a passenger and stops, reserve seats.
2. **Bookings**: open the new booking and take a payment. It turns Confirmed (payment trigger).
3. Cancel it to see the refund policy, or open a trip and use Depart then Complete trip (odometer trigger).
4. **Reports**: the five reports from `smartmove_pkg`.
5. **GPS tracking**: choose trip 1 or press Simulate journey. **Feedback**: ratings from Oracle with tags from MongoDB.
