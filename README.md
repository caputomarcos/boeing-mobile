# boeing-mobile


### Project Requirements

#### 1. **Account Creation**
   - **Registration**: Do users create accounts directly in this application, or is there integration with an existing user database?
   - **Login Options**: To streamline access, what authentication methods do we need? (e.g., Email/Password, Google, Apple)

#### 2. **Battery List**
   - **Display of Basic Information**: Each battery in the list should display key details like battery status, voltage, and perhaps charge cycles.
   - **Detailed View on Selection**: When a user selects a battery from the list, they should see additional details.

#### 3. **Battery Details**
   - **Additional Information**: What specific details should the battery detail page display? Possible data includes voltage levels, charge cycles, temperature, and operational status.
   - **Alarm Configuration**: Should alarms be configurable by the user? For instance, alarms based on low voltage, temperature thresholds, or other critical metrics.

#### 4. **Sessions**
   - **Definition of Sessions**: Are sessions related to battery usage or charging events? What key data points do we need from each session (e.g., start time, duration, peak temperature)?

#### 5. **Programs**
   - **Programs Feature for Batteries**: Should there be predefined “programs” or routines for monitoring and charging batteries? If so, what should each program include, and should it be user-customizable?

#### 6. **Settings**
   - **Battery Management**: Can users add, edit, or delete batteries from the app? Should there be any restrictions or validations?


Here’s the document reformatted in Markdown, following the specifications provided and covering the **Account Creation** and **Battery List** sections. 

---

```markdown
# SPEC-001: Battery Monitoring and Management Application

## Background

This project aims to develop a battery monitoring and management application that enables users to track battery performance metrics, manage alarms, and configure settings to maintain optimal battery health. The application will support real-time data monitoring, historical session tracking, and customizable alert notifications, ensuring comprehensive battery oversight.

## Requirements

Using MoSCoW prioritization:

- **Must Have**
  - User authentication with support for multiple login methods.
  - List and detail views for each battery, showing essential metrics.
  - Configurable alarms based on user-defined thresholds.
  - Historical session tracking for each battery.
  - Capability for users to add or remove batteries within the app.

- **Should Have**
  - Programmatic routines ("programs") for monitoring and charging configurations.
  - Notifications for alarms via app, email, and SMS.
  - A customizable dashboard to display selected battery data.

- **Could Have**
  - Integration with external systems for advanced battery diagnostics.
  - Graphical representation of battery performance trends.

- **Won't Have (for MVP)**
  - Automated troubleshooting or repair suggestions.
  - Integration with third-party battery suppliers.

## Method

The application will feature a modular architecture separating user authentication, battery data management, session tracking, and notification services. Both mobile and web platforms will be supported for broad accessibility.

### Account Creation

#### Requirements
- **User Registration and Authentication**: Users must create accounts to access battery management features, with multiple sign-in options available.
- **Login Options**: The application will support Email/Password, Google, and Apple login methods for flexibility and convenience.

#### Design Details
- **Authentication Service**: A dedicated authentication microservice will handle user accounts, using OAuth for social logins (Google, Apple) and secure password storage for Email/Password sign-ins.
- **Database Schema**: User data will be stored in a relational database. Basic schema:
  ```sql
  Table: users
  - id (UUID, Primary Key)
  - email (String, Unique)
  - password_hash (String, Nullable if social login)
  - provider (Enum: 'email', 'google', 'apple')
  - created_at (Timestamp)
  - updated_at (Timestamp)
  ```

### Battery List

#### Requirements
- **Battery Overview**: Users should see a list of all batteries, with each row displaying basic metrics like part number, serial number, voltage, and charge cycles.
- **Selection and Navigation**: Users can tap/click on a battery in the list to access additional details.

#### Design Details
- **Battery List View**: A scrollable list with rows representing individual batteries, displaying key metrics.
- **Database Schema**: Battery details will be stored in a relational database to facilitate quick querying.
  ```sql
  Table: batteries
  - id (UUID, Primary Key)
  - user_id (UUID, Foreign Key, References users)
  - part_number (String)
  - serial_number (String, Unique)
  - voltage (Float)
  - charge_cycles (Integer)
  - created_at (Timestamp)
  - updated_at (Timestamp)
  ```

- **API Endpoints**:
  - `GET /batteries`: Retrieves a list of batteries associated with the logged-in user.
  - `GET /batteries/{id}`: Retrieves detailed information for a specific battery.

- **User Interface Considerations**:
  - Basic battery metrics will be displayed in a table or card format for easy scanning.
  - Each row will include an icon or color indicator if an alarm is triggered for that battery.

## Implementation

1. **Authentication Module**:
   - Implement OAuth for Google and Apple logins.
   - Set up user registration and login flows.
   - Securely store user data in the database.

2. **Battery List Module**:
   - Develop API endpoints to fetch and display the battery list.
   - Design UI for battery list with selectable rows.
   - Connect UI to back-end to enable navigation to the battery detail view.

## Milestones

1. **Week 1-2**: Set up Authentication Module
   - Implement user registration and login methods.
   - Verify login flows for each provider (Email, Google, Apple).

2. **Week 3-4**: Develop Battery List Module
   - Implement database schema for batteries.
   - Create API endpoints for fetching and displaying battery data.
   - Design and test the battery list UI.

## Gathering Results

The system's effectiveness will be evaluated based on:

- **User Engagement**: Frequency of user logins and battery data checks.
- **Battery List Usability**: User feedback on list accessibility and navigability.
- **Authentication Reliability**: Success rate of logins and registrations across methods.
