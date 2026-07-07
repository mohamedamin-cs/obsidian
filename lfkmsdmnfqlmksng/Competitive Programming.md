bool divisibleBy7(const string& s) {
	int rem = 0;
	 for (char c : s) {
		  rem = (rem * 10 + (c - '0')) % 7;
	 }
	  return rem == 0;
 }