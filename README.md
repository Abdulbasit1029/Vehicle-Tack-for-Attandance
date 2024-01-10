# Vehicle-Tack-for-Attandance
import tkinter as tk
from datetime import datetime

class VehicleAttendanceSystem:
    def __init__(self, master):
        self.master = master
        self.master.title("Vehicle Attendance System")

        # Variables
        self.vehicle_number_var = tk.StringVar()
        self.attendance_list = []

        # GUI Components
        tk.Label(master, text="Vehicle Number:").grid(row=0, column=0, padx=10, pady=10)
        self.vehicle_entry = tk.Entry(master, textvariable=self.vehicle_number_var)
        self.vehicle_entry.grid(row=0, column=1, padx=10, pady=10)

        self.mark_attendance_button = tk.Button(master, text="Mark Attendance", command=self.mark_attendance)
        self.mark_attendance_button.grid(row=1, column=0, columnspan=2, pady=10)

        self.attendance_display = tk.Text(master, height=10, width=40)
        self.attendance_display.grid(row=2, column=0, columnspan=2, padx=10, pady=10)

    def mark_attendance(self):
        vehicle_number = self.vehicle_number_var.get()
        if vehicle_number:
            timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
            attendance_record = f"{timestamp} - Vehicle {vehicle_number} marked attendance\n"
            self.attendance_list.append(attendance_record)
            self.update_attendance_display()

    def update_attendance_display(self):
        self.attendance_display.delete(1.0, tk.END)  # Clear previous content
        for record in self.attendance_list:
            self.attendance_display.insert(tk.END, record)

def main():
    root = tk.Tk()
    app = VehicleAttendanceSystem(root)
    root.mainloop()

if __name__ == "__main__":
    main()
