**<h1>GlasGo bike-sharing system</h1>**
**<h2>Project Overview</h2>**
The shared bike system is a comprehensive platform where users can register, rent shared bikes, manage orders, and make payments; operators can manage vehicle statuses; and administrators can manage all system users and monitor operations. This system aims to provide convenient bike-sharing services, enhancing user experience while ensuring vehicle maintenance and availability.
**<h2>Installation and Setup</h2>**
* Python 3.8+
* Django 4.0+
* SQLite3

**<h3>Clone the Repository</h3>**
```python
git clone https://stgit.dcs.gla.ac.uk/programming-and-systems-development-m/2024/lb01-04/bike_sharing.git
```
**<h3>Create a Virtual Environment and Install Dependencies</h3>**
delete original venv
```python
python -m venv venv
source venv/bin/activate  # For Windows User  venv\Scripts\activate
pip install -r requirements.txt
```
**<h3>Database Migration</h3>**
```python
python manage.py makemigrations
python manage.py migrate
```
**<h3>Create a Superuser</h3>**
```python
python manage.py createsuperuser
```

**<h3>Run the Development Server</h3>**
```python
python manage.py runserver
```
Visit http://127.0.0.1:8000/ to access the homepage. Admin users can log in to /admin and assign roles as manager or operator, redirecting them to respective dashboards

**<h3>Functions Tests</h3>**
models,views,form
```python
python manage.py test evehicle
# python manage.py test
# test_results.txt
```

**<h2>Functional Overview</h2>**
**<h3>User Panel</h3>**

* **Registration and Login**
* **Rent a Bike：** After logging in, users can rent bikes via a QR code scan. The rental is charged at £0.2 per minute
* **Return a Bike：** Users can end the rental session via the "End Ride" button
* **Top-up Balance：** Users can top up their balance with £5 increments
* **Report Vehicle Status：** Users can submit vehicle conditions such as "request charging" or "request repairing" after scanning
* **Feedback：** Users can evaluate their experience with the service by providing a rating and optional comments.

**<h3>Operator Dashboard</h3>**

* **View Vehicle Status：** Operators can monitor battery levels, availability, charging, and repair status of all vehicles
* **Manage Vehicle Status：** 
  * Vehicles requiring charging or repair appear highlighted for easy identification
  * Moved vehicles are labeled with "position moved," allowing operators to reset the position to the initial location

**<h3>Manager Dashboard</h3>**

* **System Monitoring：** Managers can view and manage vehicle statuses, usage, and operational data for optimal system performance
* **Visual Reports**
  * **order duration and revenue：** The duration and amount of all rental orders
  * **vehicle location mapping：** Statistics of current vehicle locations, mapped to real Glasgow locations using latitude and longitude
  * **weekly revenue：** Daily revenue for the past week
  * **Rental Time Statistics：** Splits the day into 8 parts and counts the number of orders during each time segment
  * **top ten most-used bikes**

**<h2>Code Structure</h2>**

* **web_first/:** Main Directory 
  * **evehicle/templates:** 
    * **index:** Frontpage
    * **login:** 
    * **register:** 
    * **logout:** 
    * **profile:** Customer profile
    * **manager_dashboard:** 
    * **operator_dashoboard:**  
    * **create_rental:** Create rental order
    * **ride_tracking:** 
  * **evehicle/static:** Imgs and styles
  * **evehicle/management/commands:** enerates QR codes for vehicles
  * **evehicle/img:** QR codes
  * **evehicle/services.py:** Core Logic
  * **evehicle/views.py:** Defines request views, handling frontend requests
  * **evehicle/models.py:** Defines data models such as users, vehicles, and rental orders
  * **evehicle/forms.py:** Contains forms for registration and top-ups
  * **web_first/urls.py:** Maps specific URLs to view functions

**<h2>Operation Workflow</h2>**

**<h3>User Workflow</h3>**

* **Registration and Login：** Users can register and log in to the system using their account credentials

* **Vehicle Rental：** After logging in, users can rent a bike by clicking the "Rent a Vehicle" button, scanning the QR code on the bike to begin the session. The system charges £0.2 per minute, with real-time tracking available

* **Vehicle Return：** Once the session is over, users can click the "End Ride" button, which generates an order and deducts the rental fee

* **Top-up Balance：** Users can add £5 to their balance through the "Top Up Balance" button on the homepage

* **Report Vehicle Condition：** After scanning, users can see the bike's status and report issues by requesting charging or repairs

* **Submit Feedback：** Users can choose a score ranging from 1 to 5, with 1 indicating
poor service and 5 indicating good service.

**<h3>Operator Workflow</h3>**

* **View Vehicle Status：** Operators monitor all vehicles' current status from the control panel, including battery levels, charging needs, and repair statuses

* **Submit Status Changes：** Operators can initiate charging, repairs, or move vehicles back to their original location if moved

* **Page Redirection and Refresh：** After successful operations, pages are refreshed to display updated statuses

**<h3>Manager Workflow</h3>**

* **Manage Users and Operators：** Admins can log in to the backend to manage users and operators, adjusting permissions and status as needed

* **Monitor System Status：** Managers oversee all vehicles' statuses and usage data to ensure smooth operation

* **Generate Visualisation Reports**

**<h2>Issues and Solutions</h2>**

* **operator and manager_dashboard pages failed to load content：** 
  
  * Use incognito mode or clear the browser cache
  * Open the browser's Developer Tools under the Network tab and reload to identify what’s missing
  * For asynchronous data loading issues, move logic to services.py and call it through views