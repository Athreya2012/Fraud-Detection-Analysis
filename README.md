# Fraud-Detection-Analysis  

In collaboration with Nava Kumar Sajjan https://github.com/sajjansaju

Dataset - 
https://www.kaggle.com/datasets/amanalisiddiqui/fraud-detection-dataset?select=AIML+Dataset.csv

<h1 align="center">Hi 👋, I'm Athreya Arunachalam</h1>
<h3 align="center">A passionate Business Analyst from Sydney</h3>

- 🔭 I’m currently working on [Fraud-Detection-Analysis](https://github.com/Athreya2012/Fraud-Detection-Analysis)

- 🌱 I’m currently learning **Master of Business Analytics**

- 👯 I’m looking to collaborate on **Finance related Projects**

- 👨‍💻 All of my projects are available at [www.linkedin.com/in/athreya-arunachalam-6bb1281b0](www.linkedin.com/in/athreya-arunachalam-6bb1281b0)

- 📝 I regularly write articles on [www.linkedin.com/in/athreya-arunachalam-6bb1281b0](www.linkedin.com/in/athreya-arunachalam-6bb1281b0)

- 💬 Ask me about **SQL, Power BI**

- 📫 How to reach me **athreya201297@gmail.com**

- 📄 Know about my experiences [www.linkedin.com/in/athreya-arunachalam-6bb1281b0](www.linkedin.com/in/athreya-arunachalam-6bb1281b0)

<h3 align="left">Connect with me:</h3>
<p align="left">
<a href="https://linkedin.com/in/athreya arunachalam" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/linked-in-alt.svg" alt="athreya arunachalam" height="30" width="40" /></a>
<a href="https://instagram.com/athreya.arunachalam" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/instagram.svg" alt="athreya.arunachalam" height="30" width="40" /></a>
</p>

<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://developer.android.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/android/android-original-wordmark.svg" alt="android" width="40" height="40"/> </a> <a href="https://git-scm.com/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="git" width="40" height="40"/> </a> <a href="https://www.adobe.com/in/products/illustrator.html" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/adobe_illustrator/adobe_illustrator-icon.svg" alt="illustrator" width="40" height="40"/> </a> <a href="https://www.mathworks.com/" target="_blank" rel="noreferrer"> <img src="https://upload.wikimedia.org/wikipedia/commons/2/21/Matlab_Logo.png" alt="matlab" width="40" height="40"/> </a> <a href="https://www.mongodb.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mongodb/mongodb-original-wordmark.svg" alt="mongodb" width="40" height="40"/> </a> <a href="https://www.microsoft.com/en-us/sql-server" target="_blank" rel="noreferrer"> <img src="https://www.svgrepo.com/show/303229/microsoft-sql-server-logo.svg" alt="mssql" width="40" height="40"/> </a> <a href="https://www.mysql.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/mysql/mysql-original-wordmark.svg" alt="mysql" width="40" height="40"/> </a> <a href="https://www.oracle.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/oracle/oracle-original.svg" alt="oracle" width="40" height="40"/> </a> <a href="https://www.postgresql.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/postgresql/postgresql-original-wordmark.svg" alt="postgresql" width="40" height="40"/> </a> <a href="https://www.python.org" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/python/python-original.svg" alt="python" width="40" height="40"/> </a> <a href="https://redis.io" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/redis/redis-original-wordmark.svg" alt="redis" width="40" height="40"/> </a> <a href="https://sass-lang.com" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/sass/sass-original.svg" alt="sass" width="40" height="40"/> </a> <a href="https://www.sqlite.org/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/sqlite/sqlite-icon.svg" alt="sqlite" width="40" height="40"/> </a> </p>

--Basic Queries to understand dataset

--1)Total transactions and fraud count
select count(*) as total_transactions,
sum(isfraud) as fraud_count
from transactions;

<img width="316" alt="image" src="https://github.com/user-attachments/assets/5b29168d-8892-4061-885f-7247a3b946fb" />


--2)List of unique transaction types
select distinct type
from transactions;
<img width="218" alt="image" src="https://github.com/user-attachments/assets/119a9747-5a9c-462e-89d0-df7727328143" />


--3)Top 5 highest distinct transaction amounts
select distinct amount
from transactions
order by amount desc
limit 5;
<img width="217" alt="image" src="https://github.com/user-attachments/assets/fd9b52a7-7b04-4da5-820b-539339743ff6" />


--- Intermediate Queries to discover patters 

--4)Fraud rate by transaction type
select type,
count(isfraud) as no_of_transactions,
round(sum(isfraud)::decimal /count(*) * 100,2) as fraud_rate
from transactions
group by type;

<img width="494" alt="image" src="https://github.com/user-attachments/assets/c8545d19-b45f-4db4-9c03-ed9465132455" />


--5)Top 5 suspicious sender accounts by fraud count
select nameorig as sender_account,
count(isfraud) as no_of_fraud
from transactions
where isfraud = 1
group by sender_account
order by no_of_fraud desc
limit 5;

<img width="317" alt="image" src="https://github.com/user-attachments/assets/e4779622-9953-4bd5-a306-a00ce25771a1" />



--6)Transaction count over time (by step)
select step as unit_of_time,
count(*)
from transactions
group by unit_of_time
order by unit_of_time asc;

<img width="217" alt="image" src="https://github.com/user-attachments/assets/1641c131-8de5-4017-9bec-754f0fb2b501" />


--Advanced Queries for insights and anomaly detection

--7)Mismatch in balances (possible manipulation or allowing overdrafts and simply zeroing out balances)
select *
from transactions
where (type in ('CASH_OUT','DEBIT','PAYMENT','TRANSFER') and (oldbalanceorg <> newbalanceorig + amount)) 
or 
(type ='CASH_IN' and (oldbalanceorg <> newbalanceorig - amount));

<img width="1122" alt="image" src="https://github.com/user-attachments/assets/988e5553-5b35-412c-83a1-3f164bf33f66" />

--8)Looping or round-tripping (money goes out, then comes back in)
SELECT DISTINCT t1.nameOrig
FROM transactions t1
JOIN transactions t2
  ON t1.nameOrig = t2.nameDest
  AND t1.amount = t2.amount;

  <img width="294" alt="image" src="https://github.com/user-attachments/assets/2fb7b90c-f023-4b6f-beb5-c1847b8ee754" />


--9)Running total of frauds over time
SELECT step,
       SUM(isFraud) AS no_of_frauds,
       SUM(SUM(isFraud)) OVER (ORDER BY step) AS running_total_frauds
FROM transactions
GROUP BY step
ORDER BY step;

<img width="389" alt="image" src="https://github.com/user-attachments/assets/dda60d5f-8e44-4669-90ba-2f6199d070a4" />

--10)Most frequently targeted accounts in fraud cases
select namedest,
sum(isfraud) as times_targeted
from transactions
where isfraud = 1
group by namedest
order by times_targeted desc
limit 10;

<img width="349" alt="image" src="https://github.com/user-attachments/assets/d61de6f8-878a-44bc-9de2-42a6f6809658" />


--11)High-value fraud transactions (top 1%)
SELECT *
FROM transactions
WHERE isFraud = 1
  AND amount > (
      SELECT PERCENTILE_CONT(0.99) 
      WITHIN GROUP (ORDER BY amount)
      FROM transactions
  );
<img width="1117" alt="image" src="https://github.com/user-attachments/assets/2ade9183-29c3-427f-a193-a9b11fc2a1d1" />

