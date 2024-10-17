#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <time.h>
#include <unistd.h>

void animate() {
    int i;
    for (i = 0; i < 2; i++) {
        printf("\rLoading");
        fflush(stdout);
        usleep(500000); // wait for 0.5 seconds
        printf("\rLoading.");
        fflush(stdout);
        usleep(500000); // wait for 0.5 seconds
        printf("\rLoading..");
        fflush(stdout);
        usleep(500000); // wait for 0.5 seconds
        printf("\rLoading...");
        fflush(stdout);
        usleep(500000); // wait for 0.5 seconds
    }
    printf("\n");
}

void create_files() {
    FILE *fp_login = fopen("login.txt", "a");
    fclose(fp_login);
    FILE *fp_registration = fopen("registration.txt", "a");
    fclose(fp_registration);
    FILE *fp_donation = fopen("donation.txt", "a");
    fclose(fp_donation);
    FILE *fp_A_plus = fopen("A+.txt", "a");
    fclose(fp_A_plus);
    FILE *fp_A_minus = fopen("A-.txt", "a");
    fclose(fp_A_minus);
    FILE *fp_B_plus = fopen("B+.txt", "a");
    fclose(fp_B_plus);
    FILE *fp_B_minus = fopen("B-.txt", "a");
    fclose(fp_B_minus);
    FILE *fp_AB_plus = fopen("AB+.txt", "a");
    fclose(fp_AB_plus);
    FILE *fp_AB_minus = fopen("AB-.txt", "a");
    fclose(fp_AB_minus);
    FILE *fp_O_plus = fopen("O+.txt", "a");
    fclose(fp_O_plus);
    FILE *fp_O_minus = fopen("O-.txt", "a");
    fclose(fp_O_minus);
}
// Function to register a new user
void register_user() {
    char username[50];
    char password[50];
    char blood_group[10];
    char contact_number[15];

    printf("Enter username: ");
    scanf("%s", username);
    printf("Enter password: ");
    scanf("%s", password);
    printf("Enter blood group: ");
    scanf("%s", blood_group);
    printf("Enter contact number: ");
    scanf("%s", contact_number);

    // Check if username already exists
    FILE *fp = fopen("login.txt", "r");
    if (fp == NULL) {
        printf("Error opening file!\n");
        return;
    }

    int username_exists = 0;
    char line[100];
    while (fgets(line, sizeof(line), fp)) {
        char reg_username[50];
        sscanf(line, "%s", reg_username);

        if (strcmp(username, reg_username) == 0) {
            username_exists = 1;
            break;
        }
    }

    fclose(fp);

    if (username_exists) {
        printf("Username already exists! Please choose a different username.\n");
        printf("1. Register again\n2. Exit\n");
        int choice;
        scanf("%d", &choice);
        if (choice == 1) {
            system("cls"); // Clear the console
            register_user(); // Recursive call to register again
        } else {
            system("cls"); // Clear the console
            exit(0); // Exit the program
        }
    } else {
        // Check if contact number already exists
        FILE *fp_reg = fopen("registration.txt", "r");
        if (fp_reg == NULL) {
            printf("Error opening file!\n");
            return;
        }

        int contact_number_exists = 0;
        while (fgets(line, sizeof(line), fp_reg)) {
            char reg_contact_number[15];
            sscanf(line, "%*s %*s %*s %s", reg_contact_number);

            if (strcmp(contact_number, reg_contact_number) == 0) {
                contact_number_exists = 1;
                break;
            }
        }

        fclose(fp_reg);

        if (contact_number_exists) {
            printf("Contact number already exists! Please choose a different contact number.\n");
            printf("1. Register again\n2. Exit\n");
            int choice;
            scanf("%d", &choice);
            if (choice == 1) {
                system("cls"); // Clear the console
                register_user(); // Recursive call to register again
            } else {
                system("cls"); // Clear the console
                exit(0); // Exit the program
            }
        } else {
            // Save registration info to registration.txt file
            FILE *fp_reg = fopen("registration.txt", "a");
            if (fp_reg == NULL) {
                printf("Error opening file!\n");
                return;
            }
            fprintf(fp_reg, "%s %s %s %s\n", username, password, blood_group, contact_number);
            fclose(fp_reg);

            // Save login info to login.txt file
            FILE *fp_login = fopen("login.txt", "a");
            if (fp_login == NULL) {
                printf("Error opening file!\n");
                return;
            }
            fprintf(fp_login, "%s %s\n", username, password);
            fclose(fp_login);

            printf("Registration successful!\n");
            printf("Please login to continue...\n");
            system("cls"); // Clear the console
            printf ("Log in\n");
            login_user(); // Call login_user() after registration
        }
    }
}

// Function to login an existing user
void login_user() {
    char username[50];
    char password[50];
    char line[100];
    int found = 0;

    while (!found) {
        printf("Enter username: ");
        scanf("%s", username);
        printf("Enter password: ");
        scanf("%s", password);

        // Read login information from login.txt file
        FILE *fp = fopen("login.txt", "r");
        if (fp == NULL) {
            printf("Error opening file!\n");
            return;
        }

found = 0;
        while (fgets(line, sizeof(line), fp)) {
            char reg_username[50];
            char reg_password[50];
            sscanf(line, "%s %s", reg_username, reg_password);

            if (strcmp(username, reg_username) == 0 && strcmp(password, reg_password) == 0) {
                found = 1;
                break;
            }
        }

        fclose(fp);

        if (!found) {
            printf("Invalid username or password! Try again.\n");
            printf("1. Login again\n2. Register\n3. Exit\n");
            int choice;
            scanf("%d", &choice);
            if (choice == 1) {
                system("cls"); // Clear the console
                login_user(); // Recursive call to login again
            } else if (choice == 2) {
                system("cls"); // Clear the console
                register_user(); // Call register_user() to register a new user
            } else {
                system("cls"); // Clear the console
                exit(0); // Exit the program
            }
        }
    }

    printf("Login successful!\n");
    system("cls"); // Clear the console
    user_menu(); // Call user_menu() after login
}

// Function to display user menu
void user_menu(){
    int choice;
    while (1) {
        system("cls"); // Clear the console
        printf("1. Donate\n2. Receive\n3. Logout\n4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                donate_blood();
                break;
            case 2:
                receive_blood();
                break;
            case 3:
                printf("Logout option selected.\n");
                system("cls"); // Clear the console
                main(); // Return to main menu
                break;
            case 4:
                printf("Exiting program...\n");
                system("cls"); // Clear the console
                exit(0); // Exit the program
                break;
            default:
                printf("Invalid choice! Try again.\n");
        }
    }
}

// Function to donate blood
void donate_blood() {
    system("cls"); // Clear the console
    char date[20];
    char donor_name[100]; // Increased size to accommodate full names
    char blood_group[10];
    char last_donation_date[20];
    char mobile_number[15];
    char location[20];

    printf("Enter date (DD/MM/YYYY): ");
    scanf("%s", date);
    printf("Enter donor name: ");
    scanf(" %[^\n]", donor_name);
    printf("Enter blood group: ");
    scanf("%s", blood_group);
    printf("Enter last date of blood donation (DD/MM/YYYY): ");
    scanf("%s", last_donation_date);
    printf("Enter mobile number: ");
    scanf("%s", mobile_number);

    int location_choice;
    printf("Select a location:\n");
    printf("1. Oxygen\n");
    printf("2. 2 No. Gate\n");
    printf("3. GEC\n");
    printf("4. Muradpur\n");
    printf("5. Bahardarhat\n");
    printf("6. Agrabad\n");
    printf("7. Halishahar\n");
    printf("8. A.K Khan\n");
    printf("9. Chawkbazar\n");
    printf("Enter your choice: ");
    scanf("%d", &location_choice);

    switch (location_choice) {
        case 1:
            strcpy(location, "Oxygen");
            break;
        case 2:
            strcpy(location, "2 No. Gate");
            break;
        case 3:
            strcpy(location, "GEC");
            break;
        case 4:
            strcpy(location, "Muradpur");
            break;
        case 5:
            strcpy(location, "Bahardarhat");
            break;
        case 6:
            strcpy(location, "Agrabad");
            break;
        case 7:
            strcpy(location, "Halishahar");
            break;
        case 8:
            strcpy(location, "A.K Khan");
            break;
        case 9:
            strcpy(location, "Chawkbazar");
            break;
        default:
            printf("Invalid choice!\n");
            return;
    }

    int dd, mm, yy;
    sscanf(last_donation_date, "%d/%d/%d", &dd, &mm, &yy);

    if (checkBloodDonationAvailability(dd, mm, yy)) {
        printf("You are eligible to donate blood.\n");

        // Save donation info to donation.txt file
        FILE *fp_donation = fopen("donation.txt", "a");
        if (fp_donation == NULL) {
            printf("Error opening file!\n");
            return;
        }
        fprintf(fp_donation, "%s %s %s %s %s %s\n", date, donor_name, blood_group, last_donation_date, mobile_number, location);
        fclose(fp_donation);

        // Save donation info to corresponding blood group TXT file
        char blood_group_file[20];
        if (strcmp(blood_group, "A+") == 0) {
            strcpy(blood_group_file, "A+.txt");
        } else if (strcmp(blood_group, "A-") == 0) {
            strcpy(blood_group_file, "A-.txt");
        } else if (strcmp(blood_group, "B+") == 0) {
            strcpy(blood_group_file, "B+.txt");
        } else if (strcmp(blood_group, "B-") == 0) {
            strcpy(blood_group_file, "B-.txt");
        } else if (strcmp(blood_group, "AB+") == 0) {
            strcpy(blood_group_file, "AB+.txt");
        } else if (strcmp(blood_group, "AB-") == 0) {
            strcpy(blood_group_file, "AB-.txt");
        } else if (strcmp(blood_group, "O+") == 0) {
            strcpy(blood_group_file, "O+.txt");
        } else if (strcmp(blood_group, "O-") == 0) {
            strcpy(blood_group_file, "O-.txt");
        }

        FILE *fp_blood_group = fopen(blood_group_file, "a");
        if (fp_blood_group == NULL) {
           printf("Error opening file!\n");
            return;
        }
        fprintf(fp_blood_group, "%s %s %s %s %s %s\n", date, donor_name, blood_group, last_donation_date, mobile_number, location);
        fclose(fp_blood_group);

        printf("Donation successful!\n");
    } else {
        printf("You are not eligible to donate blood yet.\n");
    }

    printf("Press enter to continue...");
    getchar();
    getchar();
}

// Function to check blood donation availability
int checkBloodDonationAvailability(int dd, int mm, int yy) {
    struct tm tm1 = { 0 };
    tm1.tm_year = yy - 1900;
    tm1.tm_mon = mm - 1;
    tm1.tm_mday = dd;
    tm1.tm_hour = tm1.tm_min = tm1.tm_sec = 0;
    tm1.tm_isdst = -1;
    time_t t1 = mktime(&tm1);

    time_t now = time(0);

    double dt = abs(difftime(t1, now));
    int days = round(dt / 86400);

    if(days >= 90) return 1;
    else return 0;
}

// Function to receive blood
void receive_blood() {
    system("cls"); // Clear the console
    int blood_group_choice;

    printf("Select a blood group:\n");
    printf("1. A+\n");
    printf("2. A-\n");
    printf("3. B+\n");
    printf("4. B-\n");
    printf("5. AB+\n");
    printf("6. AB-\n");
    printf("7. O+\n");
    printf("8. O-\n");
    printf("Enter your choice: ");
    scanf("%d", &blood_group_choice);

    char blood_group[10];
    switch (blood_group_choice) {
        case 1:
            strcpy(blood_group, "A+");
            break;
        case 2:
            strcpy(blood_group, "A-");
            break;
        case 3:
            strcpy(blood_group, "B+");
            break;
        case 4:
            strcpy(blood_group, "B-");
            break;
        case 5:
            strcpy(blood_group, "AB+");
            break;
        case 6:
            strcpy(blood_group, "AB-");
            break;
        case 7:
            strcpy(blood_group, "O+");
            break;
        case 8:
            strcpy(blood_group, "O-");
            break;
        default:
            printf("Invalid choice!\n");
            return;
    }

    printf("You have selected %s blood group.\n", blood_group);

// Open the corresponding blood group text file
FILE *fp = fopen(strcat(strcpy(malloc(strlen(blood_group) + 3), blood_group), ".txt"), "r");
if (fp == NULL) {
    printf("Error opening file!\n");
    return;
}

system("cls"); // Clear the console
// Display available donors
printf("Available donors:\n");

char line[100];
while (fgets(line, sizeof(line), fp)) {
    printf("%s", line);
}

fclose(fp); // Close the file

    printf("1. Back to main menu\n2. Exit\n");
    int choice;
    scanf("%d", &choice);
    if (choice == 1){
        system("cls"); // Clear the console
        user_menu(); // Call user_menu() to go back to the main menu
    } else {
        system("cls"); // Clear the console
        exit(0); // Exit the program
    }
}

int main() {
    create_files();
    printf("Welcome to PROJECT ROKTIM!\n");
    animate();
    printf("Project Successfully Loaded. Starting project...\n");
    system("cls");
    int choice;
    printf("1. Register\n2. Login\n3. Exit\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);
    switch (choice) {
        case 1:
            system("cls"); // Clear the console
            register_user();
            break;
        case 2:
            system("cls"); // Clear the console
            login_user();
            break;
        case 3:
            printf("Exiting program...\n");
            system("cls"); // Clear the console
            exit(0); // Exit the program
            break;
        default:
            printf("Invalid choice!\n");
    }

    return 0;
}
