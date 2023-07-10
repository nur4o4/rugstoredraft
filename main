import java.io.*; //import for reading in file
import java.util.*; //import for arraylist
import java.util.Scanner; //import for user input
import java.io.BufferedWriter;//imports for reading and writing to txt file
import java.io.FileWriter;

//main class
class Main {
  // arraylists used throughout the program
  public static ArrayList<String> read = new ArrayList<String>();// arraylist read tex file in to
  public static ArrayList<String> rackLetter = new ArrayList<String>();// arraylist for only rack letters (A,B,C)
  public static ArrayList<Integer> rackNumber = new ArrayList<Integer>();// arraylist for only rack #s
  private static ArrayList<String> rugName = new ArrayList<String>();// arraylist for only rug names

  public static void main(String[] args) {
    System.out.println("FOR CONTEXT FOR THIS ASSIGNMENT: I work at a rug store and while working there it's always been a struggle to find where specific rugs are on our racks. Our current system tells us if we have the rug, but not where it is. This program is designed to resolve that issue.\n");//nur assignment idea info message
    Scanner keyedInput = new Scanner(System.in);// for user entry
    menu classObj = new menu();// instance of the menu class to access menu instance methods

    // reading in text file into arraylist read using buffer reader
    BufferedReader br = null;
    try {
      br = new BufferedReader(new FileReader("putup.txt"));
      String word;
      while ((word = br.readLine()) != null) {
        read.add(word.toLowerCase());//reading in all lowercase
      } //adding txt file into arrayList
    } catch (IOException e) {
      e.printStackTrace();
    } finally {
      try {
        br.close();
      } catch (IOException ex) {
        ex.printStackTrace();
      }
    }

    //adding to other arraylist from main arraylist read
    for (int i = 0; i < read.size(); i += 3) {
      rackLetter.add(read.get(i));//add all rack letters (a,b,c)
    }
    for (int i = 1; i < read.size(); i += 3) {
      rackNumber.add(Integer.parseInt(read.get(i)));//add all rack #s
    }
    for (int i = 2; i < read.size(); i += 3) {
      rugName.add(String.valueOf(read.get(i)));//add all rug names
    }

    //intro message
    System.out.println("AREA RUG SHOP - DAY 1 EMPLOYEE \nPlease enter your full name:");
    String name = keyedInput.nextLine();//input name
    System.out.println("Welcome to Area Rug Shop " + name
        + "! You will use this program to perform your daily duties. Rugs are going to be your new best friend!\nHow does the store work?\nThere are three racks. A, B and C. Rack A has spots 1-20, rack B spot 21-40 and rack C spots 41-60. Each rug has an individual name. This program is not case sensitive.");//customised intro message

    //while loop for displaying menu
    int i = 0;
    while (i == 0) {
      System.out.println("\nEnter a menu item number:\n1. Search for a rug name\n2. Enter a rug into the system\n3. See rugs in acending order per rack\n4. Exit");//menu items print
      try{//in case user doesn't enter a menu item #
      String menuChoice =   keyedInput.nextLine();//user entered item choice
      if (Integer.parseInt(menuChoice) == 1) {//if menu item 1 chosen
        menu.menu1(rugName, read);//instance method menu1 and its needed parameters
      }
      if (Integer.parseInt(menuChoice) == 2) {//if menu item 2 chosen
        menu.menu2(arr, read);//instance method menu2 and its needed parameters
      }
      if (Integer.parseInt(menuChoice) == 3) {//if menu item 3 chosen
        menu.menu3(read);//instance method menu3 and its needed parameters
      }
      if(Integer.parseInt(menuChoice)==4){//if menu item 4 chosen (exit)
        System.out.println("Have a good one!");//bye message
        i+=1;//ending while loop, ending program
      }}
      catch (Exception e) {System.out.println("Error occured, incorrect user entry. Please try again.");}//catching error made by not entering a menu item
    }
  }	
  
  //instance method, adding to the txt file for menu2
  public void tryAdd(String a, String b, String c) {

    try {
      FileWriter writer = new FileWriter("putup.txt", true);
      BufferedWriter bufferedWriter = new BufferedWriter(writer);
      //adding new entered lines
      bufferedWriter.newLine();
      bufferedWriter.write(a.toLowerCase());//rack letter
      bufferedWriter.newLine();
      bufferedWriter.write(b.toLowerCase());//rack #
      bufferedWriter.newLine();
      bufferedWriter.write(c.toLowerCase());//rug name
      bufferedWriter.close();

      // adding txt file into arrayList
    } catch (IOException e) {
      e.printStackTrace();
    }

    //rereading into txt file to add new lines
    BufferedReader br = null;
    try {
      br = new BufferedReader(new FileReader("putup.txt"));
      String word;
      while ((word = br.readLine()) != null) {
        read.add(word.toLowerCase());
      } // readding txt file into arrayList
    } catch (IOException e) {
      e.printStackTrace();
    } finally {
      try {
        br.close();
      } catch (IOException ex) {
        ex.printStackTrace();
      }
    }
    
    //updating new lines into each of the arraylists, all used later in the program
    for (int i = 0; i < read.size(); i += 3) {
      rackLetter.add(read.get(i));
    }
    for (int i = 1; i < read.size(); i += 3) {
      rackNumber.add(Integer.parseInt(read.get(i)));
    }
    for (int i = 2; i < read.size(); i += 3) {
      rugName.add(String.valueOf(read.get(i)));
    }

  }

  //instance variable arr, used as a self-updating array version of rugname arraylist
  private static String[] arr;
  public Main(String[] arr) {
    this.arr = arr;
  }

  public static String[] getArr() {
    return arr;
  }

  //binary search class method, parameters: array version of rugnames and string of rug name the user is searchng for
  public static int binarySearch(String[] arr, String x) {
    int l = 0, r = arr.length - 1;
    //loop to implement Binary Search
    while (l <= r) {
      //calculatiing mid
      int m = l + (r - l) / 2;
      int res = x.compareTo(arr[m]);
      //check if x is present at mid
      if (res == 0)
        return m;
      //if x greater, ignore left half
      if (res > 0)
        l = m + 1;
      //if x is smaller, ignore right half
      else
        r = m - 1;
    }

    return -1;
  }
}

//menu class, used for each menu items
class menu {
  //arraylists to store rug info for each of the rack letters
  public static ArrayList<Integer> A = new ArrayList<Integer>();
  public static ArrayList<Integer> B = new ArrayList<Integer>();
  public static ArrayList<Integer> C = new ArrayList<Integer>();

  //menu1 method, parameters: rugname arraylist and read arraylist
  public static void menu1(ArrayList<String> rugName1, ArrayList<String> read1) {
    Scanner keyedInput = new Scanner(System.in);// for user entry

    String[] arr = rugName1.toArray(new String[0]);//turning rugname arraylist into array arr
    Arrays.sort(arr);//sorting alphabetically

    //user enters rug to search for
    System.out.println("Enter a rug to search for:");
    String rugSearch = keyedInput.nextLine();

    //calling Main class method to search for entered rug
    int result = Main.binarySearch(arr, rugSearch.toLowerCase());

    //place of entered rug in the read arraylist, in case it's found
    int place = read1.indexOf(rugSearch.toLowerCase());
    if (result == -1) {//if not found
      System.out.println("Not found. Most likely in the back or inventory error.");
    } else {//if found
      System.out.println("Found! "
          + arr[result].toUpperCase() + " is on rack " + read1.get(place - 2).toUpperCase() + " on spot " + read1.get(place - 1));//printing in all caps for rug name and rack letter
    }//print all rug info based on int place
  }

  //menu2 method, parameter string array main class object and read arraylist
  public static void menu2(String[] arr, ArrayList<String> read1) {
    Scanner keyedInput = new Scanner(System.in);// for user entry

    Main main = new Main(arr);//instance of class

    //user entering new rug into
    System.out.println("Enter the rack letter (A,B or C):");
    String letterAdd = keyedInput.nextLine();
    System.out.println("Enter the rack number:");
    String numAdd = keyedInput.nextLine();
    System.out.println("Enter the rug name:");
    String nameAdd = keyedInput.nextLine();

    if (nameAdd.equals("")||letterAdd.equals("")||numAdd.equals("")){//if a blank user entry
      System.out.println("Cannot enter a blank field. Please try again.");//print can't be done
    }
    else{
   try{//trying in case the numAdd entered is not an integer and causes erre
     			Integer.parseInt(numAdd); 
if(letterAdd.toLowerCase().equals("a")||letterAdd.toLowerCase().equals("b")||letterAdd.toLowerCase().equals("c")){
    //checking if rug entered already in system
    int printable = 0;
    for (int i = 0; i<read1.size(); i++){
if(letterAdd.equals(read1.get(i))&&numAdd.equals(read1.get(i+1))){//equals rug spot filled in the system
        System.out.println("This spot is already filled.");
        printable +=1;//not printable
      }
    } 
    if (printable == 0){//if not already in system, add it
    main.tryAdd(letterAdd.toLowerCase(), numAdd, nameAdd.toLowerCase());//calling tryAdd in main to add new info to txt file
    System.out.println(nameAdd.toUpperCase() + " on rack " + letterAdd.toUpperCase() + " at spot " + numAdd + " added!");}//printing finished message
  }}
  catch(Exception e){//error caused, user entry not correct
    System.out.println("Incorrect user entry");
  }}}
      
  //menu3 method, parameter arraylist read
  public static void menu3(ArrayList<String> read1) {
    Scanner keyedInput = new Scanner(System.in);// for user entry

    System.out.println("Enter a rack letter to see rugs hung up in numerical order (A,B or C)");//info message
    String letterSort = keyedInput.nextLine();//which rack user wants to see info for

    //Adding all rug numbers on rack A into arraylist A
    for (int i = 0; i < read1.size(); i++) {
      if (read1.get(i).equals("A")||read1.get(i).equals("a")) {
        A.add(Integer.parseInt(read1.get(i + 1).toLowerCase()));
      }
      
    //Adding all rug numbers on rack B into arraylist B
      if (read1.get(i).equals("B")||read1.get(i).equals("b")) {
        B.add(Integer.parseInt(read1.get(i + 1).toLowerCase()));
      }

    //Adding all rug numbers on rack C into arraylist C
      if (read1.get(i).equals("C")||read1.get(i).equals("c")) {
        C.add(Integer.parseInt(read1.get(i + 1).toLowerCase()));
      }
    }

    //clearing any duplicated in rack # arraylists due to looping
    Set<Integer> setA = new LinkedHashSet<>();
    setA.addAll(A);
    A.clear();
    A.addAll(setA);
    Set<Integer> setB = new LinkedHashSet<>();
    setB.addAll(B);
    B.clear();
    B.addAll(setB);
    Set<Integer> setC = new LinkedHashSet<>();
    setC.addAll(C);
    C.clear();
    C.addAll(setC);

    //turning rack # arraylists into arrays
    Integer[] Aarr = A.toArray(new Integer[0]);
    Integer[] Barr = B.toArray(new Integer[0]);
    Integer[] Carr = C.toArray(new Integer[0]);

    //printing all sorted rack info for each rack
    //if user entered A AKA wants to see rack A info
    if (letterSort.toUpperCase().equals("A")) {
      System.out.println("rack # - rug");//instructions for print
      selectionSort(Aarr);//sort rug #'s in rack A
      for (int i = 0; i < Aarr.length; i++) {
        int r = read1.indexOf(Integer.toString(Aarr[i]));
        System.out.println(Aarr[i] + " - " + read1.get(r + 1).toUpperCase());//print each rug # and name
      }
    }
    //same code as rack A, for rack B
    if (letterSort.toUpperCase().equals("B")) {
          System.out.println("rack # - rug");//instructions for print
      selectionSort(Barr);
      for (int i = 0; i < Barr.length; i++) {
        int r = read1.indexOf(Integer.toString(Barr[i]));
        System.out.println(Barr[i] + " " + read1.get(r + 1).toUpperCase());
      }
    }
    //same code as rack A, for rack C
    if (letterSort.toUpperCase().equals("C")) {
          System.out.println("rack # - rug");//instructions for print
      selectionSort(Carr);
      for (int i = 0; i < Carr.length; i++) {
        int r = read1.indexOf(Integer.toString(Carr[i]));
        System.out.println(Carr[i] + " " + read1.get(r + 1).toUpperCase());
      }
    }
  }

  //selection sort used for menu3, parameter integer array being sorted
  public static void selectionSort(Integer[] a) {
    int i, j, minV, minI, temp = 0;// variables/counters
    for (i = 0; i < a.length; i++) {// main loop
      minV = a[i];// setting minimum value
      minI = i;
      for (j = i; j < a.length; j++) {// comparison loop
        if (a[j] < minV) {// if minV is greater than the num
          minV = a[j];
          minI = j;
        }
      }
      if (minV < a[i]) {// if the num is greater than the minimum value, shift it and have new minimum
                        // value
        temp = a[i];// swapping
        a[i] = a[minI];
        a[minI] = temp;
      }
    }
  }

}
