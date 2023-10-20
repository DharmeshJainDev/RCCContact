# Contact Syncing

> Fetch contact from device and sync them to coreData , realm or BE via socket

## Models

ContactCardModel
- This model is used with multipe init show we can convert CNContact , RealmPhoneContact , CoreConatact and variable toDictionary is used convert the data json so we can sent it to BE

RealmPhoneContact
- It has same properties of ContactCardModel of persisted type with contactID as primary key

CoreContact
- It's also have same properties and is used for single contact and as we required to save and fetch all contacts at a time we will be using CoreContactArr

## Views
ShowContactsVC
- This is initial view controller of this RCC it has multiple buttons and of uploading contact , fetching contact , request permission , fetching filtered contact and retry fetching contacts from phone


## Controllers

RCC_Contact_Controller
- This is the main controller for communicating between phone contact and application 
- It has various function like
    1) func checkForContactpermission()
       => will call another function on the basis of contact permission in setting exists or not
    2) func requestAccess() 
       => will show alert contact native alert permission set from info plist . So that from now in app setting we will be contact permission option
    3) func authorizeStatus()
       => will check if user status for contact that user has given permission or not and fetch contact or show alert according to it
    4) func getKeyDescriptor()
       => will return CNDescriptor array values which are required details of contact store in phone
    5) func fetchContacts()
       => will fetch all the contacts from phone and pass those contacts via allContactsFetchedFromPhonebook()
    6) func getAllPhoneNumberofaContact()
       => will get all phone number of a contact
    7) func gelAllEmailofaContact()
        => will get all email address of a contact
    8) func showSettingsPopUp()
        => will show alert for contact permission not given by user
    9)  func getPredicateContact 
        => Will fetch only filter contact from whose details are given 
    - func getContactofEmail
    - func getContactofName
    - func getContactofPhoneNumber

SocketHelper
- This helper class is use for socket releated functionality having socket connection and sending data in chunck functions
    1) func sendContacts()
       => Will send all contacts in a chunk
    2) func saveUpdatedContacts()
       => will first fetch contacts from BE via get api and then only emit contacts which are not present in BE

AppNetworking
- This is for api call to get all the contacts emiitted via socket
    1) func getContactFromBE()
        => will give all contactlist as a closure
        
RealmDataBaseHelper
- This class is used for all realmDb interaction 
    1) func saveAllContacts
        => Will save all the contacts fetched from phone 
    2) func getAllContacts
        => will get all the contacts which were stores in realmDB 
    3) func saveUpdatedContacts(contacts:
        => It will first get all the contacts which are stored in realm and then save new as well as modified contact in realmdb
        
CoreDataBaseHelper
    1) func saveSingleContact
        => will save single contact in CoreDataBase
    1) func saveAllContacts
        => Will save all the contacts fetched from phone 
    2) func getAllContacts
        => will get all the contacts which were stores in CoreDataBase 
    3) func saveUpdatedContacts(contacts:
        => It will first get all the contacts which are stored in CoreDataBase and then save new as well as modified contact in CoreDataBase
