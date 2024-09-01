# EventRegistration Smart Contract
The EventRegistration contract is a smart contract designed for managing event registrations on the Ethereum blockchain. It allows an organizer to open and close registration, register participants, and manage the list of registered participants. This contract also includes functionality for retrieving participant details and removing participants if needed.
## Features
* Open/Close Registration: The organizer can control when the registration is open or closed.
* Register Participants: Users can register for the event if registration is open and the event is not fully booked.
* Remove Participants: The organizer can remove registered participants if necessary.
* Retrieve Participant Information: Retrieve individual participant details or a list of all registered participants.
## Contract Details
* Event Name: string public eventName
* Organizer: address public organizer
* Max Participants: uint public maxParticipants
* Registration Count: uint public registrationCount
* Registration Status: bool public registrationOpen
## Getting Started
### Executing Program
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

Once you are on the Remix website, create a new file by clicking on the "+" icon in the left-hand sidebar. Save the file with a .sol extension (e.g., avax.sol). Copy and paste the following code into the file:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

contract EventRegistration {
    string public eventName;
    address public organizer;
    uint public maxParticipants;
    uint public registrationCount;
    bool public registrationOpen;

    struct Participant {
        string name;
        string email;
        bool registered;
    }

    mapping(address => Participant) public participants;
    address[] public participantAddresses;  // Array to track participant addresses

    // Events
    event RegistrationOpened(uint maxParticipants);
    event RegistrationClosed();
    event ParticipantRegistered(address indexed participant, string name);
    event ParticipantRemoved(address indexed participant);
    
    constructor(string memory _eventName, uint _maxParticipants) {
        organizer = msg.sender;
        eventName = _eventName;
        maxParticipants = _maxParticipants;
        registrationCount = 0;
        registrationOpen = false;
    }

    modifier onlyOrganizer() {
        require(msg.sender == organizer, "Only the organizer can call this function");
        _;
    }

    modifier onlyWhenOpen() {
        require(registrationOpen, "Registration is not open");
        _;
    }

    modifier onlyWhenClosed() {
        require(!registrationOpen, "Registration is still open");
        _;
    }

    function openRegistration() public onlyOrganizer onlyWhenClosed {
        registrationOpen = true;
        emit RegistrationOpened(maxParticipants);
    }

    function closeRegistration() public onlyOrganizer onlyWhenOpen {
        registrationOpen = false;
        emit RegistrationClosed();
    }

    function register(string memory _name, string memory _email) public onlyWhenOpen {
        require(!participants[msg.sender].registered, "Already registered");
        require(registrationCount < maxParticipants, "Event is fully booked");

        participants[msg.sender] = Participant(_name, _email, true);
        participantAddresses.push(msg.sender);  // Add participant address to the array
        registrationCount++;
        emit ParticipantRegistered(msg.sender, _name);
    }

    function removeParticipant(address _participant) public onlyOrganizer onlyWhenClosed {
        require(participants[_participant].registered, "Participant not registered");

        // Find and remove participant from the array
        for (uint i = 0; i < participantAddresses.length; i++) {
            if (participantAddresses[i] == _participant) {
                participantAddresses[i] = participantAddresses[participantAddresses.length - 1];
                participantAddresses.pop();
                break;
            }
        }

        delete participants[_participant];
        registrationCount--;
        emit ParticipantRemoved(_participant);
    }

    function getParticipant(address _participant) public view returns (string memory name, string memory email) {
        require(participants[_participant].registered, "Participant not registered");
        Participant memory participant = participants[_participant];
        return (participant.name, participant.email);
    }

    function getAllParticipants() public view onlyOrganizer returns (Participant[] memory) {
        Participant[] memory allParticipants = new Participant[](registrationCount);
        for (uint i = 0; i < participantAddresses.length; i++) {
            address participantAddress = participantAddresses[i];
            if (participants[participantAddress].registered) {
                allParticipants[i] = participants[participantAddress];
            }
        }
        return allParticipants;
    }
}
```
### Usage
1. Deployment: Deploy the contract with the event name and maximum number of participants.
2. Open Registration: The organizer calls openRegistration() to start accepting registrations.
3. Register: Participants can call register() to sign up for the event.
4. Close Registration: The organizer can call closeRegistration() to stop accepting new registrations.
5. Manage Participants: The organizer can remove participants as needed and view all registered participants.

## Author
Vageshwari Chaudhary vageshwari1062@gmail.com

## License
This contract is licensed under the MIT License. See the LICENSE file for details.









