# [Calendars](https://lightoj.com/problem/calendars)

# 🧠 Problem Summary (Very Simple Explanation)

Different fantasy calendars exist.

Each calendar:

Has p months.

Each month has mi days.

No leap years, no special rules.

All calendars start on the same first day → 1-1-1.

You are asked:

👉 Convert a date from Calendar c1 → Calendar c2.
# 💡 Key Idea

If all calendars start on the same day,
then any date can be converted like this:

# 1️⃣ Convert given date → total days passed since 1-1-1

For calendar c1 and date (day, month, year):
```sql
days passed in previous years = (year − 1) × days_in_one_year_of_c1
days passed in previous months
days passed in current month (day - 1)
```
# 2️⃣ Convert total days into calendar c2 format

Reverse the process:
```sql
Find year, month, day of that ‘total days’ in c2
```

That’s it.

## 📘 Sample:
```sql
Calendar 1: (10, 20, 30) → Year length = 60
Calendar 2: (20, 30, 10, 20) → Year length = 80
```
Convert Calendar 1, date:
```sql
18-2-2
```
Steps:

Days before year 2 → (2−1) × 60 = 60

Month 1 = 10 days

Current month: (18−1) = 17

Total = 60 + 10 + 17 = 87 days passed

Now convert 87 days to Calendar 2:

One year = 80 days

So day 87 → year = 2

Remaining: 87 % 80 = 7

Month 1 has 20 days → 7 < 20, so month = 1

Day = 7+1 = 8

👉 Result = 8 1 2

Matches sample.

# 🧾 Now Code Explanation (Your Code)
Reading calendars
```cpp
int NC;
cin >> NC;
vector<vector<int>> Calender(NC + 1);
vector<int> yDays(NC + 1);
```

Calender[i] stores the month lengths of calendar i.

yDays[i] stores total number of days in one year of calendar i.

Reading each calendar:
```cpp
for (int i = 1; i <= NC; i++) {
    int p;
    cin >> p;
    Calender[i].resize(p + 1);
    yDays[i] = 0;
    for (int j = 1; j <= p; j++) {
        cin >> Calender[i][j];
        yDays[i] += Calender[i][j];
    }
}
```

You read p = number of months

Resize vector to 1-indexed

Sum all month lengths to compute days in a year for this calendar

## 📌 Processing Queries
```cpp
int q;
cin >> q;

Loop for each query
for (int i = 1; i <= q; i++) {
    int c1, c2, d, m, y;
    cin >> c1 >> c2 >> d >> m >> y;
```
### Step 1 → Convert c1 date into total days
```cpp
long long PassDays = 0;

PassDays += (long long) yDays[c1] * (y - 1);  // whole previous years

PassDays += (d - 1);  // previous days in current month
```

Then add all months before month m:
```cpp
for (int month = 1; month < m; month++)
    PassDays += Calender[c1][month];
```

Now PassDays = total days passed before this date.

### Step 2 → Convert total days into c2 date
Compute year:
```cpp
long long yyyy = (PassDays / yDays[c2]) + 1;
PassDays %= yDays[c2];
```
Compute month:
```cpp
int mm = 1;
while (PassDays >= Calender[c2][mm] && mm < Calender[c2].size()) {
    PassDays -= Calender[c2][mm];
    mm++;
}
```
Remaining is day
```cpp
int dd = PassDays + 1;
```
Print result
```cpp
cout << "Query " << i << ": " << dd << ' ' << mm << ' ' << yyyy << endl;
```
