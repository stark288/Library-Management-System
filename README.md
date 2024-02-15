# Library Management System based on java 
Overview :
The Library Management System is a console-based application designed to facilitate the management of library resources, including books, patrons, and transactions. It aims to automate library operations such as book cataloguing, patron registration, borrowing and returning books, and managing fines and penalties
Functional Requirements
1.	Book Management:
•	Maintain a database of library books, including details such as title, author, ISBN, genre, and availability status.
•	Allow librarians to add, update, and delete book records, including cataloging new acquisitions and removing outdated items.
•	Implement mechanisms to track book loans, reservations, and returns.
2.	Patron Management:
•	Maintain a database of library patrons, including personal details, contact information, and membership status.
•	Allow librarians to register new patrons, update patron records, and manage membership renewals or cancellations.
•	Implement authentication mechanisms to ensure secure patron access to library services.
3.	Book Borrowing and Returning:
•	Enable patrons to search for available books, check out books, and request book reservations.
•	Track borrowed books, due dates, and overdue fines for each patron.
•	Implement checkout and return workflows, including barcode scanning or manual entry of book IDs.
4.	Fines and Penalties Management:
•	Calculate and track fines for overdue books based on predefined penalty rules.
•	Notify patrons of overdue books and pending fines through reminders and notifications.
•	Allow librarians to manage fine payments, waivers, and adjustments.
5.	Catalog Search and Navigation:
•	Provide patrons with search functionality to find books by title, author, genre, or other criteria.
•	Implement browsing features such as browsing by category, new arrivals, or popular titles.

# the package names are :
1.Package: com.librarymanagement.person
2.com.librarymanagement.membership
3. com.librarymanagement.account
4. com.librarymanagement.book
5. com.librarymanagement.transaction.records
5 a. com.librarymanagement.transaction.finance
6.com.librarymanagement.activity
7.com.librarymanagement.library
8.com.librarymanagement.utils
9.com.librarymanagement.exceptions

9. BookNotFoundException: Thrown when a requested book is not found in the catalogue.

PatronNotFoundException: Thrown when a patron's details are not found in the system.

InvalidBookOperationException: Thrown for operations that are not allowed on a book, such as trying to borrow a book that is already checked out.

AuthenticationException: Thrown when a user fails to authenticate, such as entering an incorrect password or username.

AuthorizationException: Thrown when a user attempts to perform an action they are not permitted to do, such as a patron trying to add a new book.

OverdueBookException: Thrown when a book is overdue and a patron attempts to borrow another book, if the system's policy restricts this.

MembershipExpiredException: Thrown when a patron with an expired membership tries to use library services.

DatabaseConnectionException: Thrown when the system is unable to establish a connection to the database.

DataValidationException: Thrown when input data does not pass validation checks.

FinePaymentException: Thrown when there is an issue with processing a fine payment, such as insufficient funds or an invalid payment method.






#The methods , fields , constructors required to Implement the Library System 

Person
Fields:

private String name;
private String email;
Constructors:

public Person(String name, String email)
Methods:

public void updatePersonalDetails(String name, String email)
public static Person fromDBModel(ResultSet rs)
public HashMap<String, Object> toDBModel()
Account
Fields:

private String username;
private String password;
private LocalDateTime lastLoginTime; // For tracking login time
private LocalDateTime lastLogoutTime; // For tracking logout time
Constructors:

public Account(String username, String password)
Methods:

public boolean login(String username, String password) // Updated to record login time
public void logout() // Updated to record logout time
public boolean changePassword(String oldPassword, String newPassword)
private boolean verifyCredentials()
Librarian (Inherits from Person)
Fields:

private Account account;
Constructors:

public Librarian(String name, String email, Account account)
Methods:

public void addBook(Book book)
public void updateBook(Book book)
public void deleteBook(String isbn)
public void registerPatron(Patron patron)
public void updatePatron(Patron patron)
public void collectFine(Patron patron, double amount)
private void saveLibrarianToDB()
private void updateLibrarianInDB()
private void deleteLibrarianFromDB()
Patron (Inherits from Person)
Fields:

private Account account;
private Membership membership;
Constructors:

public Patron(String name, String email, Account account, Membership membership)
Methods:

public List<Book> searchBook(String criteria)
public void borrowBook(Book book)
public void returnBook(ReturnBook returnBook)
public void reserveBook(Book book)
public void payFine(double amount)
private void savePatronToDB()
private void updatePatronInDB()
private void deletePatronFromDB()
Membership
Fields:

private String membershipId;
private LocalDate startDate;
private LocalDate endDate;
private String status;
Constructors:

public Membership(String membershipId, LocalDate startDate, LocalDate endDate, String status)
Methods:

public void renewMembership()
public void cancelMembership()
private void saveMembershipToDB()
private void updateMembershipStatusInDB()
Book
Fields:

private String isbn;
private String title;
private Author author;
private String genre;
private String availabilityStatus;
Constructors:

public Book(String isbn, String title, Author author, String genre, String availabilityStatus)
Methods:

public void updateAvailabilityStatus(String status)
private void saveBookToDB()
private void updateBookInDB()
private void deleteBookFromDB()
public void checkout()
public void reserve()
Author
Fields:

private String authorId;
private String name;
Constructors:

public Author(String authorId, String name)
Methods:

public void updateAuthorDetails(String name)
private void saveAuthorToDB()
private void updateAuthorInDB()
Catalogue
Fields:

private List<Book> books;
Constructors:

public Catalogue(List<Book> books)
Methods:

public void addBook(Book book)
public void removeBook(String isbn)
public List<Book> searchBooks(String criteria)
private void loadCatalogFromDB()
private void updateCatalogInDB()
BorrowBook
Fields:

private String borrowId;
private Book book;
private Patron patron;
private LocalDate borrowDate;
private LocalDate dueDate;
Constructors:

public BorrowBook(String borrowId, Book book, Patron patron, LocalDate borrowDate, LocalDate dueDate)
Methods:

public void extendDueDate(LocalDate newDueDate)
private void saveBorrowRecordToDB()
private void updateBorrowRecordInDB()
ReturnBook
Fields:

private String returnId;
private BorrowBook borrow;
private LocalDate returnDate;
Constructors:

public ReturnBook(String returnId, BorrowBook borrow, LocalDate returnDate)
Methods:

public void processReturn()
private void saveReturnRecordToDB()
public double calculateFine()
Reservation
Fields:

private String reservationId;
private Book book;
private Patron patron;
private LocalDate reservationDate;
private String status;
Constructors:

public Reservation(String reservationId, Book book, Patron patron, LocalDate reservationDate, String status)
Methods:

public void cancelReservation()
public void confirmReservation()
private void saveReservationToDB()
private void updateReservationStatusInDB()
Fine
Fields:

private String fineId;
private double amount;
private String description;
Constructors:

public Fine(String fineId, double amount, String description)
Methods:

public void updateFineAmount(double newAmount)
private void saveFineToDB()
private void updateFineInDB()
Payment
Fields:

private String paymentId;
private double amount;
private LocalDate paymentDate;
private String paymentMethod;
Constructors:

public Payment(String paymentId, double amount, LocalDate paymentDate, String paymentMethod)
Methods:

public void processPayment()
public void refundPayment()
private void processPaymentInDB()
private void refundPaymentInDB()
Library
Fields:

private String libraryId;
private String name;
private String address;
private List<Librarian> librarians;
private List<Patron> patrons;
private Catalogue catalogue;
Constructors:

public Library(String libraryId, String name, String address, List<Librarian> librarians, List<Patron> patrons, Catalogue catalogue)
Methods:

public void addLibrarian(Librarian librarian)
public void removeLibrarian(String librarianId)
public void addPatron(Patron patron)
public void removePatron(String patronId)
public void updateLibraryDetails(String name, String address)
private void loadLibraryDetailsFromDB()
private void updateLibraryDetailsInDB()
public List<UserActivity> getUserActivities(int userId) // Retrieve activities for a specific user
public List<UserActivity> getAllUserActivities() // Retrieve all user activities for reporting
UserActivity (New Class for Tracking Activities)
Fields:

private int userId;
private String activityType; // e.g., "Login", "Search", "Checkout"
private String activityDetails; // e.g., book ID, search query
private LocalDateTime timestamp; // The date and time when the activity occurred
Constructors:

public UserActivity(int userId, String activityType, String activityDetails)
Methods:

public void logActivity() // Method to log the activity to the database









# the overall package and code combination is

Package: com.librarymanagement.person

Class: Person

Fields:
private String name;
private String email;
Constructors:
public Person(String name, String email)
Methods:
public void updatePersonalDetails(String name, String email)
public static Person fromDBModel(ResultSet rs)
public HashMap<String, Object> toDBModel()


Class: Librarian (Inherits from Person)

Fields:
private Account account;
Constructors:
public Librarian(String name, String email, Account account)
Methods:
public void addBook(Book book)
public void updateBook(Book book)
public void deleteBook(String isbn)
public void registerPatron(Patron patron)
public void updatePatron(Patron patron)
public void collectFine(Patron patron, double amount)
private void saveLibrarianToDB()
private void updateLibrarianInDB()
private void deleteLibrarianFromDB()
// Additional methods for managing reservations and stock as mentioned in previous messages

Class: Patron (Inherits from Person)

Fields:
private Account account;
private Membership membership;
Constructors:
public Patron(String name, String email, Account account, Membership membership)
Methods:
public List<Book> searchBook(String criteria)
public void borrowBook(Book book)
public void returnBook(ReturnBook returnBook)
public void reserveBook(Book book)
public void payFine(double amount)
private void savePatronToDB()
private void updatePatronInDB()
private void deletePatronFromDB()

Package: com.librarymanagement.membership

Class: Membership
Fields:
private String membershipId;
private LocalDate startDate;
private LocalDate endDate;
private String status;
Constructors:
public Membership(String membershipId, LocalDate startDate, LocalDate endDate, String status)
Methods:
public void renewMembership()
public void cancelMembership()
private void saveMembershipToDB()
private void updateMembershipStatusInDB()


Package: com.librarymanagement.account

Class: Account
Fields:
private String username;
private String password;
private LocalDateTime lastLoginTime;
private LocalDateTime lastLogoutTime;
Constructors:
public Account(String username, String password)
Methods:
public boolean login(String username, String password)
public void logout()
public boolean changePassword(String oldPassword, String newPassword)
private boolean verifyCredentials()


Package: com.librarymanagement.book

Class: Book

Fields:
private String isbn;
private String title;
private Author author;
private String genre;
private String availabilityStatus;
Constructors:
public Book(String isbn, String title, Author author, String genre, String availabilityStatus)
Methods:
public void updateAvailabilityStatus(String status)
private void saveBookToDB()
private void updateBookInDB()
private void deleteBookFromDB()
public void checkout()
public void reserve()

Class: Author

Fields:
private String authorId;
private String name;
Constructors:
public Author(String authorId, String name)
Methods:
public void updateAuthorDetails(String name)
private void saveAuthorToDB()
private void updateAuthorInDB()
Class: Catalogue

Fields:
private List<Book> books;
Constructors:
public Catalogue(List<Book> books)
Methods:
public void addBook(Book book)
public void removeBook(String isbn)
public List<Book> searchBooks(String criteria)
private void loadCatalogFromDB()
private void updateCatalogInDB()



Package: com.librarymanagement.transaction.records

Class: BorrowBook

Fields:
private String borrowId;
private Book book;
private Patron patron;
private LocalDate borrowDate;
private LocalDate dueDate;
Constructors:
public BorrowBook(String borrowId, Book book, Patron patron, LocalDate borrowDate, LocalDate dueDate)
Methods:
public void extendDueDate(LocalDate newDueDate)
private void saveBorrowRecordToDB()
private void updateBorrowRecordInDB()


Class: ReturnBook

Fields:
private String returnId;
private BorrowBook borrow;
private LocalDate returnDate;
Constructors:
public ReturnBook(String returnId, BorrowBook borrow, LocalDate returnDate)
Methods:
public void processReturn()
private void saveReturnRecordToDB()
public double calculateFine()


Class: Reservation

Fields:
private String reservationId;
private Book book;
private Patron patron;
private LocalDate reservationDate;
private String status;
Constructors:
public Reservation(String reservationId, Book book, Patron patron, LocalDate reservationDate, String status)
Methods:
public void cancelReservation()
public void confirmReservation()
private void saveReservationToDB()
private void updateReservationStatusInDB()


Package: com.librarymanagement.transaction.finance

Class: Fine

Fields:
private String fineId;
private double amount;
private String description;
Constructors:
public Fine(String fineId, double amount, String description)
Methods:
public void updateFineAmount(double newAmount)
private void saveFineToDB()
private void updateFineInDB()


Class: Payment

Fields:
private String paymentId;
private double amount;
private LocalDate paymentDate;
private String paymentMethod;
Constructors:
public Payment(String paymentId, double amount, LocalDate paymentDate, String paymentMethod)
Methods:
public void processPayment()
public void refundPayment()
private void processPaymentInDB()
private void refundPaymentInDB()


Package: com.librarymanagement.activity

Class: UserActivity
Fields:
private int userId;
private String activityType;
private String activityDetails;
private LocalDateTime timestamp;
Constructors:
public UserActivity(int userId, String activityType, String activityDetails)
Methods:
public void logActivity()


Package: com.librarymanagement.library

Class: Library
Fields:
private String libraryId;
private String name;
private String address;
private List<Librarian> librarians;
private List<Patron> patrons;
private Catalogue catalogue;
Constructors:
public Library(String libraryId, String name, String address, List<Librarian> librarians, List<Patron> patrons, Catalogue catalogue)
Methods:
public void addLibrarian(Librarian librarian)
public void removeLibrarian(String librarianId)
public void addPatron(Patron patron)
public void removePatron(String patronId)
public void updateLibraryDetails(String name, String address)
private void loadLibraryDetailsFromDB()
private void updateLibraryDetailsInDB()
public List<UserActivity> getUserActivities(int userId)
public List<UserActivity> getAllUserActivities()
Package: com.librarymanagement.utils

Utility classes would be listed here with their respective fields and methods.
Package: com.librarymanagement.exceptions

Custom exception classes would be listed here with their respective fields and methods.






