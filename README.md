#include <iostream>
#include <vector>
using namespace std;
const int TOTAL_COACHES = 6;
const int SEATS_PER_COACH = 80;
const int EXTRA_COACHES_LAST_TRAIN = 2;
const int RETURN_TICKET_COST = 25;
struct TrainJourney {
    int passengersBooked;
    int moneyCollected;
};
int main() {
    vector<TrainJourney> journeysUp(4);
    vector<TrainJourney> journeysDown(4);
    for (int i = 0; i < 4; ++i) {
        journeysUp[i].passengersBooked = 0;
        journeysUp[i].moneyCollected = 0;
        journeysDown[i].passengersBooked = 0;
        journeysDown[i].moneyCollected = 0;
    }
    int availableSeats[4] = {TOTAL_COACHES * SEATS_PER_COACH, TOTAL_COACHES * SEATS_PER_COACH, TOTAL_COACHES * SEATS_PER_COACH, (TOTAL_COACHES + EXTRA_COACHES_LAST_TRAIN) * SEATS_PER_COACH};
    int totalPassengers = 0;
    int totalMoney = 0;
    int maxPassengers = 0;
    int maxPassengersIndex = -1;
    while (true) {
        int passengers, trainTime, ticketChoice;
        cout << "Enter the number of passengers (1-480) or '0' to exit: ";
        cin >> passengers;
        if (passengers == 0) {
            break;
        }
        if (passengers < 1 || passengers > 480) {
            cout << "Invalid number of passengers. Please enter a value between 1 and 480." << endl;
            continue;
        }
        cout << "Enter the train time (9, 11, 13, 15): ";
        cin >> trainTime;
        if (trainTime != 9 && trainTime != 11 && trainTime != 13 && trainTime != 15) {
            cout << "Invalid train time. Please enter a valid time." << endl;
            continue;
        }
        int returnTrainTime = (trainTime + 1) % 24;
        int trainIndex = (trainTime - 9) / 2;
        if (trainTime == 11) {
            trainIndex = 1; 
        }
        cout << "Do you want tickets for the journey up (1), down (2), or both (3)?: ";
        cin >> ticketChoice;
        int ticketCost = 0;
        if (ticketChoice == 1 || ticketChoice == 3) {
            if (availableSeats[trainIndex] >= passengers) {
                availableSeats[trainIndex] -= passengers;
                int remainingPassengers = passengers;
                int freeTickets = remainingPassengers / 10;
                remainingPassengers -= freeTickets;
                int singleJourneyCost = remainingPassengers * RETURN_TICKET_COST;
                journeysUp[trainIndex].passengersBooked += passengers;
                journeysUp[trainIndex].moneyCollected += singleJourneyCost;
                totalPassengers += passengers;
                totalMoney += singleJourneyCost;
                if (passengers > maxPassengers) {
                    maxPassengers = passengers;
                    maxPassengersIndex = trainIndex;
                }
                ticketCost += singleJourneyCost;
                cout << "Tickets booked for " << passengers << " passengers for the journey up." << endl;
                cout << freeTickets << " passengers travel for free on the journey up." << endl;
            } else {
                cout << "Journey up is full! Tickets cannot be booked for this journey." << endl;
            }
        }
        if (ticketChoice == 2 || ticketChoice == 3) {
            if (availableSeats[trainIndex] >= passengers) {
                availableSeats[trainIndex] -= passengers;
                int remainingPassengers = passengers;
                int freeTickets = remainingPassengers / 10;
                remainingPassengers -= freeTickets;
                int singleJourneyCost = remainingPassengers * RETURN_TICKET_COST;
                journeysDown[trainIndex].passengersBooked += passengers;
                journeysDown[trainIndex].moneyCollected += singleJourneyCost;
                totalPassengers += passengers;
                totalMoney += singleJourneyCost;

                if (passengers > maxPassengers) {
                    maxPassengers = passengers;
                    maxPassengersIndex = trainIndex;
                }
                ticketCost += singleJourneyCost;
                cout << "Tickets booked for " << passengers << " passengers for the journey down." << endl;
                cout << freeTickets << " passengers travel for free on the journey down." << endl;
            } else {
                cout << "Journey down is full! Tickets cannot be booked for this journey." << endl;
            }
        }
        cout << "Total cost for the selected journey(s): $" << ticketCost << endl;
    }
    cout << "\nTotals for Journeys Up (Passengers / Money Collected):" << endl;
    for (int i = 0; i < 4; ++i) {
        cout << "Journey " << (i + 1) << ": " << journeysUp[i].passengersBooked << " / $" << journeysUp[i].moneyCollected << endl;
    }
    cout << "\nTotals for Journeys Down (Passengers / Money Collected):" << endl;
    for (int i = 0; i < 4; ++i) {
        cout << "Journey " << (i + 1) << ": " << journeysDown[i].passengersBooked << " / $" << journeysDown[i].moneyCollected << endl;
    }
    cout << "\nTotal Passengers for the day: " << totalPassengers << endl;
    cout << "Total Money Collected for the day: $" << totalMoney << endl;
    if (maxPassengersIndex != -1) {
        cout << "The most popular journey of the day is Train " << (maxPassengersIndex + 1) << " with " << maxPassengers << " passengers." << endl;
    } else {
        cout << "No journeys were made today." << endl;
    }
    return 0;
}
