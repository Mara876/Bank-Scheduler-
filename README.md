 
 
 import datetime
import time

class Customer:
    def __init__(self, name, phone_number, appointment_time):
        self.name = name
        self.phone_number = phone_number
        self.appointment_time = appointment_time

class Bank:
    def __init__(self, name, address, phone_number):
        self.name = name
        self.address = address
        self.phone_number = phone_number
        self.appointments = []
    
    def add_appointment(self, customer):
        self.appointments.append(customer)
    
    def send_alert(self, customer):
        current_time = datetime.datetime.now()
        time_until_appointment = customer.appointment_time - current_time
        minutes_until_appointment = round(time_until_appointment.total_seconds() / 60)
        if minutes_until_appointment == 15:
            print(f"Hi {customer.name}, your appointment at {self.name} is in 15 minutes. Please be ready!")
    
    def run_appointment_system(self):
        while True:
            name = input("Please enter your name: ")
            phone_number = input("Please enter your phone number: ")
            appointment_date_str = input("Please enter your appointment date and time (YYYY-MM-DD HH:MM): ")
            appointment_date = datetime.datetime.strptime(appointment_date_str, '%Y-%m-%d %H:%M')
            customer = Customer(name, phone_number, appointment_date)
            self.add_appointment(customer)
            print("Thank you, your appointment has been scheduled.")
            while True:
                answer = input("Would you like to schedule another appointment? (Y/N): ")
                if answer.upper() == "Y":
                    break
                elif answer.upper() == "N":
                    return
                else:
                    print("Please enter Y or N.")
    
    def start_alerts(self):
        while True:
            for customer in self.appointments:
                self.send_alert(customer)
            time.sleep(60)
                
bank = Bank("Bank of Example", "Main St Santa Cruz.", "St.Elizabeth")
bank.run_appointment_system()
bank.start_alerts()
