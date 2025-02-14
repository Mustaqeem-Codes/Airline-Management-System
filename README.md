![logo](![Airline-Reservation-System](https://github.com/user-attachments/assets/2965d41f-da06-4cbc-89e1-ff7dceaa1c50)

# Airline-Management-System in C++
#include <iostream> // Libraries
#include <conio.h>
#include <fstream>
using namespace std;

void Welcome()
{
    system("cls");
    cout << endl;
    cout << endl;
    cout << "   **       **      **  ********  **            ******     *******    **            **  ******** " << endl;
    cout << "   **     **  **    **  **        **          **         **       **  ** **      ** **  **       " << endl;
    cout << "   **   **      **  **  ********  **          **         **       **  **  **    **  **  ******** " << endl;
    cout << "   ** **         ** **  **        **          **         **       **  **   **  **   **  **       " << endl;
    cout << "   **               **  ********  *********     ******     *******    **     **     **  ******** " << endl;
    cout << "            ^                                                                ^                   " << endl;
    cout << "           | |             ***************   *********                      | |                  " << endl;
    cout << "     **####   ####**             **        **         **              **####   ####**            " << endl;
    cout << "       *###   ###*               **      **             **              *###   ###*              " << endl;
    cout << "          || ||                  **     **               **                || ||                 " << endl;
    cout << "          || ||                  **      **             **                 || ||                 " << endl;
    cout << "       **##   ##**               **        **         **                **##   ##**              " << endl;
    cout << "           ###                   **          *********                      ###                  " << endl;
    cout << "                   ***************************************************** " << endl;
    cout << "                    A I R L I N E    M A N A G E M E N T    S Y S T E M  " << endl;
    cout << "                   ***************************************************** " << endl;
}

void Header()
{
    cout << "***************************************************** " << endl;
    cout << " A I R L I N E    M A N A G E M E N T    S Y S T E M  " << endl;
    cout << "***************************************************** " << endl;
}

int LogIn()
{
    int LogInOption;
    cout << "*-*-*-*-*-*     M a i n     M e n u      *-*-*-*-*-*" << endl;
    cout << "1-Log in as Admin" << endl;
    cout << "2-Log in as Ticket Booker" << endl;
    cout << "3-Exit " << endl;
    cout << "Your Option: ";
    cin >> LogInOption;
    return LogInOption;
}

void Signup2()
{
    fstream file;
    file.open("Booker.txt", ios::out);
    cout << "Enter username: ";
    string username;
    cin >> username;
    cout << "Enter password: ";
    string password;
    cin >> password;
    file << username << endl;
    file << password << endl;
    cout << "Account created successfully, Now log in for execution " << endl;
    cout << endl;
    file.close();
}

bool Signin2()
{
    fstream file;
    string fileuser;
    string filepass;
    file.open("Booker.txt", ios::in);
    cout << "Enter username: ";
    string username;
    cin >> username;
    cout << "Enter password: ";
    string password;
    cin >> password;
    file >> fileuser;
    file >> filepass;
    if (username == fileuser && password == filepass)
    {
        return 1;
    }
    else
    {
        return 0;
    }
}

int Admin(int n)
{
    int AdminOption;
    cout << "***************************************************** " << endl;
    cout << "           A d m i n   M a i n   M e n u              " << endl;
    cout << "***************************************************** " << endl;
    cout << " Main Menu > Admin Menu   " << endl;
    cout << "1-Arrangement of Flights  " << endl;
    cout << "2-View Passengers Record  " << endl;
    cout << "3-   Staff Schedule       " << endl;
    cout << "4-New Staff Recruitment   " << endl;
    cout << "5- Ticket Cancellation    " << endl;
    cout << "6-        Exit            " << endl;
    cout << "Select an option: ";
    cin >> AdminOption;
    return AdminOption;
}

void flightSchedule(int &currentFlights, int maxFlights, int time[], string destination[])
{
    fstream flightsFile;
    flightsFile.open("flights.txt", ios::app);

    if (!flightsFile)
    {
        cerr << "Error opening file!" << endl;
        return;
    }

    while (currentFlights < maxFlights)
    {
        cout << "Enter " << currentFlights + 1 << " flight time (in 24-hour format, e.g., 1300 for 1:00 PM): ";
        cin >> time[currentFlights];
        cout << "Enter Destination: ";
        getline(cin, destination[currentFlights]);

        // Save the current flight details to the file
        flightsFile << "Flight " << currentFlights + 1 << "\n"
                    << "Time: " << time[currentFlights] << "\n"
                    << "Destination: " << destination[currentFlights] << "\n\n";

        currentFlights++;

        cout << "Flight time and destination updated successfully!" << endl;

        // Prompt to continue or exit
        cout << "Do you want to add another flight? (y/n): ";
        char choice;
        cin >> choice;
        if (choice == 'n' || choice == 'N')
        {
            break;
        }
    }

    flightsFile.close(); // Close the file
    cout << "All flight details saved successfully." << endl;
}

void passengerRecord(int &currentPassenger, int cnic[], string name[], string gender[], int age[], string destination[], int seat[])
{
    if (currentPassenger == 0)
    {
        cout << "No Passenger record yet " << endl;
        cout << "Press any key to continue: ";
        getch();
    }
    else
    {
        system("cls");
        Header();
        cout << "Main menu > Admin Menu > Passenger record " << endl;
        cout << "CNIC          Name          Age          Gender          Destination          Seat Number" << endl;
        for (int i = 0; i < currentPassenger; i++)
        {
            cout << cnic[i] << "          " << name[i] << "           " << age[i] << "             " << gender[i] << "               " << destination[i] << "                  " << seat[i] << endl;
        }
        cout << "Press any key to continue: ";
        getch();
    }
}

void staffSchedule(int newStaff, int &currentFlights, int &currentCount)
{
    int n = 36;
    n += newStaff;
    int totalStaff[n];
    int sum = 0;
    for (int i = currentCount; i < currentFlights; i++)
    {
        cout << "Enter staff number for " << i + 1 << " flight: ";
        cin >> totalStaff[i];
        sum += totalStaff[i];
        if (sum > n)
        {
            cout << "Staff limit reached " << endl;
            cout << "Kindly update staff number!!" << endl;
            cout << "Press any key to continue: ";
            getch();
            break;
        }
        else
        {
            cout << "Staff number added successfully." << endl;
            cout << "Press any key to continue: ";
            getch();
            currentCount++;
            break;
        }
    }
}

void cancelTicket(int currentFlights, string destination[], int currentPassenger, int cnic[], string name[], int age[], string gender[], int seat[])
{
    cout << "Enter Destination: ";
    string cancelDestination;
    cin >> cancelDestination;
    bool validDestination = false;
    for (int i = 0; i < currentFlights; i++)
    {
        if (cancelDestination == destination[i])
        {
            validDestination = true;
            break;
        }
    }
    if (!validDestination)
    {
        cout << "Invalid destination entered!!" << endl;
        cout << "Press any key to continue: ";
        getch();
        return;
    }
    bool found = false;
    cout << "Enter CNIC of passenger: ";
    int cancel;
    cin >> cancel;
    for (int j = 0; j < currentPassenger; j++)
    {
        if (cancel == cnic[j])
        {
            cnic[j] = 0000;
            name[j] = "Cancelled";
            age[j] = 00;
            gender[j] = "---";
            seat[j] = 00;

            found = true;
            cout << "Ticket successfully canceled for CNIC: " << cancel << endl;
            break;
        }
    }

    if (!found)
    {
        cout << "No passenger record found for CNIC: " << cancel << endl;
    }
    cout << "Press any key to continue: ";
    getch();
}

void displayFlights(int currentFlights, int time[], string destination[])
{
    if (currentFlights == 0)
    {
        cout << "Flight schedule not available yet " << endl;
        cout << "Press any key to continue: ";
        getch();
    }
    else
    {
        cout << "flight time           Destination" << endl;
        for (int i = 0; i < currentFlights; i++)
        {
            cout << "  " << time[i] << " : 00      " << "          " << destination[i] << endl;
        }
        cout << "Press any key to continue: ";
        getch();
    }
}

int Booker(int num)
{
    int BookerOption;
    cout << "********************************************** " << endl;
    cout << " T I C K E T   B O O K E R   M a i n   M e n u " << endl;
    cout << "***********************************************" << endl;
    cout << "Main Menu > Booker Menu" << endl;
    cout << "1-View Fligt Schedule" << endl;
    cout << "2-Ticket Booking" << endl;
    cout << "3-Ticket Cancellation " << endl;
    cout << "4-View Passengers Record" << endl;
    cout << "5-Exit" << endl;
    cout << "Select an option: ";
    cin >> BookerOption;
    return BookerOption;
}

void ticketBooking(int &currentPassenger, int maxPassenger, int cnic[], string name[], string gender[], int age[], int seat[])
{
    fstream ticket;
    ticket.open("Ticket Booking.txt", ios::app);

    if (!ticket)
    {
        cerr << "Error opening file!" << endl;
        return;
    }

    while (currentPassenger < maxPassenger)
    {
        cout << "Enter Passenger CNIC: ";
        cin >> cnic[currentPassenger];
        cout << "Enter Passenger Name: ";
        cin >> name[currentPassenger];
        cout << "Enter Passenger Age: ";
        cin >> age[currentPassenger];
        cout << "Enter Passenger Gender: ";
        cin >> gender[currentPassenger];

        bool seatTaken;
        do
        {
            seatTaken = false;
            cout << "Enter Seat Number: ";
            cin >> seat[currentPassenger];
            for (int k = 0; k < currentPassenger; k++)
            {
                if (seat[currentPassenger] == seat[k])
                {
                    cout << "Seat Already Booked. Please choose another." << endl;
                    seatTaken = true;
                    break;
                }
            }
        } while (seatTaken);

        cout << "Seat reserved successfully!" << endl;
        ticket << "CNIC: " << cnic[currentPassenger] << "\t"
               << "Name: " << name[currentPassenger] << "\t"
               << "Age: " << age[currentPassenger] << "\t"
               << "Gender: " << gender[currentPassenger] << "\t"
               << "Seat: " << seat[currentPassenger] << "\n";
        currentPassenger++;
        cout << "Enter any key to continue: ";
        getch();
        break;
    }

    ticket.close();
    cout << "All booking details saved successfully." << endl;
}

void End()
{
    cout << endl;
    cout << "Thank you for using my Program" << endl;
    cout << endl;
    cout << " ##########     ##         ##   ## ###    " << endl;
    cout << " ##             ##  ##     ##   ##    ##  " << endl;
    cout << " ##########     ##    ##   ##   ##    ##  " << endl;
    cout << " ##             ##      ## ##   ##    ##  " << endl;
    cout << " ##########     ##         ##   ## ###    " << endl;
    cout << endl;
    cout << "         Program Ends         " << endl;
    cout << endl;
}

int main()
{
    int choice = 0, pass;
    int adminChoice = 0;
    int bookerChoice = 0;
    int maxFlights = 3;
    int currentFlights = 0;
    int time[maxFlights];
    string destination[maxFlights];
    string PassengerDestination;

    int currentPassenger = 0;
    const int maxPassenger = 30;
    int age[maxPassenger];
    int cnic[maxPassenger];
    string name[maxPassenger];
    string gender[maxPassenger];
    int seat[maxPassenger];
    int currentCount = 0;
    Welcome();
    Header();
    while (true)
    {
        choice = LogIn();
        if (choice == 1)
        {
            string adminpass;
            cout << "Enter Password: ";
            cin >> adminpass;
            if (adminpass == "Admin@123")
            {
                while (true)
                {
                    int newStaff;
                    system("cls");
                    adminChoice = Admin(pass);
                    if (adminChoice == 1)
                    {
                        system("cls");
                        Header();
                        cout << "Main menu > Admin Menu > Arrangement of Flights " << endl;
                        if (currentFlights == maxFlights)
                        {
                            cout << "Flights limit reached!! " << endl;
                            cout << "Press any key to continue: ";
                            getch();
                        }
                        else
                        {
                            flightSchedule(currentFlights, maxFlights, time, destination);
                        }
                    }
                    else if (adminChoice == 2)
                    {
                        system("cls");
                        Header();
                        cout << "Main menu > Admin Menu > Passenger record " << endl;
                        passengerRecord(currentPassenger, cnic, name, gender, age, destination, seat);
                    }
                    else if (adminChoice == 3)
                    {
                        system("cls");
                        Header();
                        cout << "Main menu > Admin Menu > Staff Schedule " << endl;
                        if (currentFlights == 0)
                        {
                            cout << "Flights not scheduled yet!! " << endl;
                            cout << "Press any key to continue: ";
                            getch();
                        }
                        else
                        {
                            staffSchedule(newStaff, currentFlights, currentCount);
                        }
                    }
                    else if (adminChoice == 4)
                    {
                        system("cls");
                        Header();
                        cout << "Main menu > Admin Menu > Staff Recruitment " << endl;
                        cout << "Enter number of new staff recruitment: ";
                        cin >> newStaff;
                        cout << newStaff << "New Staff added successfully!" << endl;
                        cout << "Press any key to continue: ";
                        getch();
                    }
                    else if (adminChoice == 5)
                    {
                        system("cls");
                        Header();
                        cout << "Main menu > Admin Menu > Cancel a ticket " << endl;
                        cancelTicket(currentFlights, destination, currentPassenger, cnic, name, age, gender, seat);
                    }
                    else if (adminChoice == 6)
                    {
                        break;
                    }
                    else
                    {
                        cout << "Invalid input, Try again " << endl;
                        cout << "Press any key to continue: ";
                        getch();
                        continue;
                    }
                }
            }
            else
            {
                cout << "Incorrect username or password " << endl;
                cout << "Press any key to continue: ";
                getch();
                system("cls");
                Header();
                cout << endl;
                continue;
            }
        }
        else if (choice == 2)
        {
            system("cls");
            Header();
            cout << "1-Signup " << endl;
            cout << "2-Log in " << endl;
            cout << "Enter a choice: ";
            int BookChoice;
            cin >> BookChoice;
            if (BookChoice == 1)
            {
                system("cls");
                Header();
                Signup2();
            }
            else if (BookChoice == 2)
            {
                system("cls");
                Header();
                bool ad = Signin2();
                if (ad)
                {
                    cout << "User Found successfully " << endl;
                    system("cls");
                    while (true)
                    {
                        system("cls");
                        bookerChoice = Booker(pass);
                        if (bookerChoice == 1)
                        {
                            system("cls");
                            Header();
                            cout << "Main menu > Booker Menu > View Flights Schedule " << endl;
                            displayFlights(currentFlights, time, destination);
                        }
                        else if (bookerChoice == 2)
                        {
                            system("cls");
                            Header();
                            cout << "Main menu > Booker Menu > Ticket Booking " << endl;
                            cout << "Enter Passenger Destination: ";
                            cin >> PassengerDestination;
                            bool found = false;
                            for (int i = 0; i < currentFlights; i++)
                            {
                                if (PassengerDestination == destination[i])
                                {
                                    found = true;
                                    ticketBooking(currentPassenger, maxPassenger, cnic, name, gender, age, seat);
                                    break;
                                }
                            }
                            if (!found)
                            {
                                cout << "Sorry, Today no flight for " << PassengerDestination << endl;
                                cout << "Press any key to continue: ";
                                getch();
                            }
                        }
                        else if (bookerChoice == 3)
                        {
                            system("cls");
                            Header();
                            cout << "Main menu > Booker Menu > Cancel a ticket " << endl;
                            cancelTicket(currentFlights, destination, currentPassenger, cnic, name, age, gender, seat);
                        }
                        else if (bookerChoice == 4)
                        {
                            system("cls");
                            Header();
                            cout << "Main menu > Admin Menu > Passenger record " << endl;
                            passengerRecord(currentPassenger, cnic, name, gender, age, destination, seat);
                            system("cls");
                        }
                        else if (bookerChoice == 5)
                        {
                            break;
                        }
                        else
                        {
                            cout << "Invalid input, Try again " << endl;
                            cout << "Press any key to continue: ";
                            getch();
                            continue;
                        }
                    }
                }
                else
                {
                    cout << "Incorrect Password " << endl;
                    cout << "Press any key to continue: ";
                    getch();
                    continue;
                }
            }
            else
            {
                cout << "Invalid Input! Try again " << endl;
                cout << "Press any key to continue: ";
                getch();
                continue;
            }
        }
        else if (choice == 3)
        {
            End();
            break;
        }
        else
        {
            cout << "Invalid input, Try again " << endl;
            cout << "Press any key to continue: ";
            getch();
            system("cls");
            continue;
        }
    }
}
