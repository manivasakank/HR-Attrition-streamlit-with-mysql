# HR-Attrition-streamlit-with-mysql
![hr1](https://github.com/user-attachments/assets/afd78536-d930-468f-b291-b5576b0a902b)
![hr2](https://github.com/user-attachments/assets/ad6c20e3-9041-4fc5-86b5-59deae9840bb)
<img width="705" height="335" alt="hr3" src="https://github.com/user-attachments/assets/7ded71ac-6940-460a-ad6b-323536938b74" />


import streamlit as st

import mysql.connector
import pandas as pd
from tabulate import tabulate
from streamlit_option_menu import option_menu

# Database connection
import mysql.connector

con = mysql.connector.connect(
    host="localhost",
    user="root",
    password="mani12",
    database="attrition"
)


osm = con.cursor()

def get_Empid():
    cus_id_lst=[]
    cus_id_qry="select Empid from employee_attrition"
    osm.execute(cus_id_qry)
    data1=osm.fetchall()
    for i in data1:
        cus_id_lst.append(i[0])
    return cus_id_lst

def get_Department():
    cus_Department_lst=[]
    qry="select department from employee_attrition"
    osm.execute(qry)
    data2=osm.fetchall()
    for i in data2:
        cus_Department_lst.append(i[0])
    return cus_Department_lst



def attrition_updates(Attrition,Department,JobRole,MonthlyIncome,Quantity):
    qry="update employee_attrition set Attrition=%s,Department=%s,JobRole=%s,MonthlyIncome=%s,Quantity=%s where Empid=%s"
    val4=(Attrition,Department,JobRole,MonthlyIncome,Quantity,Empid)
    osm.execute(qry,val4)
    con.commit()  


def employee_attrition_signup():
        EmpIDid = st.number_input("Enter the Customer Id",min_value=1,step=1)
        user_name = st.text_input("User Name",placeholder="Enter the user name")

        user_password = st.text_input("User Password",placeholder="Enter the user password",type="password")

if st.button("Customer Signup", key="customer_signup_btn"):
        
        EmpID ,Age,AgeGroup=st.columns(3)
        EmpID = EmpID.text_input("EmpID",placeholder="Enter Your EmpID")
        age = Age.text_input("Age",placeholder="Enter Your Age")
        age_group=AgeGroup.selectbox("Age Group",["","18-25","26-35","36-45","46-55"],placeholder="Enter Your Age Group")

        Attrition ,BusinessTravel=st.columns(2)
        Attrition =Attrition.selectbox("Attrition",["","Yes","No"],placeholder="Enter the Attrition")
        BusinessTravel=BusinessTravel.selectbox("Business Travel",["","Travel_Frequently","Travel_Rarely","Non-Travel"],placeholder="Enter Your Business Travel")

        DailyRate,Department=st.columns(2)
        DailyRate=DailyRate.number_input("Daily Rate",placeholder="Enter Your Daily Rate")
        Department=Department.selectbox("Department",["","Human Resources","Research & Development","Sales"],placeholder="Enter Your Department")
      

        DistanceFromHome,Education=st.columns(2)
        DistanceFromHome=DistanceFromHome.number_input("Distance From Home",placeholder="Enter Your Distance From Home")
        Education=Education.number_input("Education",placeholder="Enter Your Education")    
        
        EducationField,EmployeeCount=st.columns(2)
        EducationField=EducationField.selectbox("Education Field",["","Human Resources","Life Sciences","Marketing","Medical","Other","Technical Degree"],placeholder="Enter Your Education Field")
        EmployeeCount=EmployeeCount.number_input("Employee Count",placeholder="Enter Your Employee Count")
       

        EmployeeNumber,EnvironmentSatisfaction =st.columns(2)
        EmployeeNumber=EmployeeNumber.number_input("Employee Number",placeholder="Enter Your Employee Number")
        EnvironmentSatisfaction=EnvironmentSatisfaction.number_input("Environment Satisfaction",placeholder="Enter Your Environment Satisfaction")

        Gender,HourlyRate,JobInvolvement=st.columns(3)
        gender=Gender.selectbox("Gender",["","Male","Female"],placeholder="Enter Your Gender")
        HourlyRate=HourlyRate.number_input("Hourly Rate",placeholder="Enter Your Hourly Rate")
        JobInvolvement=JobInvolvement.number_input("Job Involvement",placeholder="Enter Your Job Involvement")

        JobLevel,JobRole,JobSatisfaction=st.columns(3)
        JobLevel=JobLevel.number_input("Job Level",placeholder="Enter Your Job Level")  
        JobRole=JobRole.selectbox("Job Role",["","Healthcare Representative","Human Resources","Laboratory Technician","Manager","Manufacturing Director","Research Director","Research Scientist","Sales Executive","Sales Representative"],placeholder="Enter Your Job Role") 
        JobSatisfaction=JobSatisfaction.number_input("Job Satisfaction",placeholder="Enter Your Job Satisfaction")
        
        MaritalStatus,MonthlyIncome=st.columns(2)
        MaritalStatus=MaritalStatus.selectbox("Marital Status",["","Divorced","Married","Single"],placeholder="Enter Your Marital Status")
        MonthlyIncome=MonthlyIncome.number_input("Monthly Income",placeholder="Enter Your Monthly Income")
        
        MonthlyRate,NumCompaniesWorked=st.columns(2)
        MonthlyRate=MonthlyRate.number_input("Monthly Rate",placeholder="Enter Your Monthly Rate")
        NumCompaniesWorked=NumCompaniesWorked.number_input("Num Companies Worked",placeholder="Enter Your Num Companies Worked")
        
        over18,overTime,PercentSalaryHike =st.columns(3)
        over18=over18.selectbox("Over 18",["","Yes","No"],placeholder="Enter Your Over 18")
        overTime = overTime.selectbox("Over Time",["","Yes","No"],placeholder="Enter Your Over Time")
        PercentSalaryHike=PercentSalaryHike.number_input("Percent Salary Hike",placeholder="Enter Your Percent Salary Hike")
       
        PerformanceRating,RelationshipSatisfaction,StandardHours=st.columns(3)
        PerformanceRating=PerformanceRating.number_input("Performance Rating",placeholder="Enter Your Performance Rating")
        RelationshipSatisfaction=RelationshipSatisfaction.number_input("Relationship Satisfaction",placeholder="Enter Your Relationship Satisfaction")
        StandardHours=StandardHours.number_input("Standard Hours",placeholder="Enter Your Standard Hours")

        StockOptionLevel,TotalWorkingYears,TrainingTimesLastYear=st.columns(3)
        StockOptionLevel=StockOptionLevel.number_input("Stock Option Level",placeholder="Enter Your Stock Option Level")
        TotalWorkingYears=TotalWorkingYears.number_input("Total Working Years",placeholder="Enter Your Total Working Years")
        TrainingTimesLastYear=TrainingTimesLastYear.number_input("Training Times Last Year",placeholder ="Enter Your Training Times Last Year") 

        WorkLifeBalance,YearsAtCompany,YearsInCurrentRole=st.columns(3)
        WorkLifeBalance=WorkLifeBalance.number_input("Work Life Balance",placeholder="Enter Your Work Life Balance")
        YearsAtCompany=YearsAtCompany.number_input("Years At Company",placeholder="Enter Your Years At Company")
        YearsInCurrentRole=YearsInCurrentRole.number_input("Years In Current Role",placeholder="Enter Your Years In Current Role")  

        YearsSinceLastPromotion,YearsWithCurrManager=st.columns(2)
        YearsSinceLastPromotion=YearsSinceLastPromotion.number_input("Years Since Last Promotion",placeholder="Enter Your Years Since Last Promotion")
        YearsWithCurrManager=YearsWithCurrManager.number_input("Years With Curr Manager",placeholder="Enter Your Years With Curr Manager")  
        
        if st.button("Sign Up",key="emp_attrition_signup_btn"):
            if not EmpID:
                st.error("Fill your EmpID")
            else:
                qry="insert into employee_attrition(EmpID,Age,AgeGroup,Attrition,BusinessTravel,DailyRate,Department,DistanceFromHome,Education,EducationField,EmployeeCount,EmployeeNumber,EnvironmentSatisfaction,Gender ,HourlyRate,JobInvolvement,JobLevel,JobRole,JobSatisfaction,MaritalStatus,MonthlyIncome,MonthlyRate,NumCompaniesWorked,over18,OverTime,PercentSalaryHike,PerformanceRating,RelationshipSatisfaction,StandardHours,StockOptionLevel,TotalWorkingYears,TrainingTimesLastYear,WorkLifeBalance,YearsAtCompany,YearsInCurrentRole,YearsSinceLastPromotion,YearsWithCurrManager)values(%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s,%s)"
                val2=(EmpID,age,age_group,attrition,business_travel,daily_rate,department,distance_from_home,education,education_field,employee_count,employee_number,environment_satisfaction,gender,hourly_rate,job_involvement,job_level,job_role,job_satisfaction,marital_status,monthly_income,monthly_rate,num_companies_worked,o18,overtime,percent_salary_hike,performance_rating,relationship_satisfaction,standard_hours,stock_option_level,total_working_years,training_times_last_year,work_life_balance,years_at_company,years_in_current_role,years_since_last_promotion,years_with_curr_manager)
                osm.execute(qry,val2)
                con.commit()
                st.success("Employee Attrition Data Inserted Successfully")
                st.balloons()           


        check = st.checkbox("I Agreed", key="agree_checkbox")

        button=st.button("Sign Up")

        if check and button:    
            attrition_updates(EmpID,Attrition,Department,JobRole,MonthlyIncome,Quantity)
            st.success("✅ Updated Successfully")   

        else:
            st.error("Please Agree to the Terms and Conditions")


    
st.image("employee-attrition2.jpg", caption="My Image", width=850)
st.title(" Employee Attrition Management System")   

st.sidebar.markdown("""
    <div style="text-align: center;">
        <h4>HR Attrition System</h4>
    </div>""",
    unsafe_allow_html=True
)
menu = st.sidebar.radio(
    "HR Attrition Menu", 
    ["Employee Attrition Signup","Update Employee Attrition"], 
    key="main_menu" 
    
)   
st.sidebar.image("employee-attrition-cover.webp", caption="My Image", width=300)
st.sidebar.video("WhatsApp Video 2026-02-05 at 12.40.04 AM.mp4")
# ---------------- Employee Attrition Signup ----------------
if menu == "Employee Attrition Signup":
    st.header("Employee Attrition Signup") 
    st.image("images (3).jpg", width=700)
employee_attrition_signup()
# ---------------- Update Employee Attrition ----------------
if menu == "Update Employee Attrition":
    st.header("Update Employee Attrition") 
    st.image("Employee-Attrition.png", width=700)
    Empid = st.selectbox(
        "Select Empid",
        get_Empid()
    ) 
    Department = st.selectbox(
        "Select Department",
        get_Department()
    ) 
    Attrition = st.selectbox(
        "Select Attrition",
        ["Yes","No"]
    ) 
    JobRole = st.text_input("Job Role") 
    MonthlyIncome = st.number_input("Monthly Income") 
    Quantity = st.number_input("Quantity") 
    check = st.checkbox("I Agreed")
    button=st.button("Update") 
    if check and button:    
        st.image("Employee-Attrition.png", width=700)
        attrition_updates(Empid,Attrition,Department,JobRole,MonthlyIncome,Quantity)
        st.success("✅ Updated Successfully")   
    else:
        st.error("Please Agree to the Terms and Conditions")
   
