vault-door-training

Approach
Inspected the provided VaultDoorTraining.java source file to determine how user input is verified.

Solution
Located the checkPassword method, 
which performed a direct string comparison against a plaintext string literal after stripping the academy{ wrapper

public boolean checkPassword(String password) {
    return password.equals("w4rm1ng_Up_w1tH_jAv4_1633b42d7f1");
}

Flag
academy{w4rm1ng_Up_w1tH_jAv4_1633b42d7f1}

Takeaway
Always inspect decompiled source code for raw string comparisons before attempting reverse engineering.
