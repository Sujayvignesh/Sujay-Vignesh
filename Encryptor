public class Encryptor {

    public static String encryptString(String input, int key) {
        StringBuilder encryptedString = new StringBuilder();

        for (char c : input.toCharArray()) {
            if (Character.isLetter(c)) {
                int charValue = Character.toLowerCase(c) - 'a';
                int encryptedValue = (charValue + key) % 26;
                char encryptedChar = (char) (encryptedValue + 'a');

                if (Character.isLowerCase(c)) {
                    encryptedChar = Character.toUpperCase(encryptedChar);
                } else {
                    encryptedChar = Character.toLowerCase(encryptedChar);
                }

                encryptedString.append(encryptedChar);
            } else {
                encryptedString.append(c); 
            }
        }

        return encryptedString.toString();
    }

    public static void main(String[] args) {
        String input1 = "Wipro Tech"; 
        int key = 20; 
        String encryptedString = encryptString(input1, key);
        System.out.println("Encrypted words: " + encryptedString);
    }
}
