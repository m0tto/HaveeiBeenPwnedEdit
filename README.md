# HaveeiBeenPwnedEdit

/*********************************************************************************************************************/

  public static void main (String[] args) {

    // Initial variables and code setup
    HaveIBeenPwnedApiClient client = new HaveIBeenPwnedApiClient("df47212e0f47445db4a8c9e9e810038d");

    String masterPass;
    boolean loggedIn;

    int count = 0;
    String pass;
    final int ATTEMPTS = 5;
    boolean isPassPwned;

    Scanner input = new Scanner(System.in);

    // Requests first password change and tests it
    System.out.print("Your password has expired. Please enter a new password: ");
    pass = input.next();
    System.out.println("");

    isPassPwned = client.isPasswordPwned(pass);

    /* Loop for testing and/or setting the new password */
    while(true) {
      // If the password HAS been pwned, request another password
      if (isPassPwned == true && count < ATTEMPTS) {
        count++;

        // Requests another password change and tests it
        System.out.print("Sorry, this password is not secure. For attempt " + count + " (out of " + ATTEMPTS + "), please enter a new password: ");
        pass = input.next();
        System.out.println("");

        isPassPwned = client.isPasswordPwned(pass);

        continue;
      }

      // If password has NOT been pwned, set it as the new password
      else if (isPassPwned == false) {
        masterPass = pass;
        System.out.println("Password meets requirements and is secure. Password updated successfully.");
        loggedIn = true;
        break;
      }

      // If count is greater than the attempt limit, display that the user has reached the limit on password change attempts and log them off
      else if(count > ATTEMPTS) {
        System.out.println("You have exceeded password change attempts and are being logged off.");
        loggedIn = false;
        System.out.println("You are now logged off.");
        break;
      }

      // Else statement not necessary, only here to complete the if statement
      else {
        System.out.println("ERROR");
        loggedIn = false;
        break;
      }
    }
    // End of loop
  }
}
