```
import java.util.ArrayList;
import java.util.Scanner;

public class MergeSorter {
    static int sortCount = 0;
    public static void merge(int[] array, int i, int j, int k)
    {
        int totalSize = k - i+1; //Size of the merged halves
        int[] mergedArray = new int[totalSize]; //New temporary array
        int insert; //Position of the value getting sorted in
        int left;  //Element of lower value position
        int right; //Element of higher value position

        insert = 0;
        left = i;
        right = j+1;
        //Add the smallest number from the left or right to the merged array
        while(left <= j && right <= k)
        {
            if(array[left] < array[right])
            {
                mergedArray[insert] = array[left];
                ++left;
            }
            else
            {
                mergedArray[insert] = array[right];
                ++right;
            }
            ++insert;
        }

        //If the left side isn't empty, add the elements to the merged array
        while(left <= j)
        {
            mergedArray[insert] = array[left];
            ++left;
            ++insert;
        }
        //Same process, but with the right side
        while(right <= k)
        {
            mergedArray[insert] = array[right];
            ++right;
            ++insert;
        }
        //Copy back to the original array
        for(insert = 0; insert < totalSize; ++insert)
        {
            array[i + insert] = mergedArray[insert];
        }
        sortCount++;
        if(mergedArray.length == array.length) {
            System.out.print("Sorted: ");
            for (int h = 0; h < mergedArray.length; h++) {
                System.out.print(mergedArray[h] + " ");
            }
            System.out.println("Comparisons: " + sortCount);
        }
    }
    public static void mergeSort(int[] array, int i, int k)
    {
        int j;


        if(i < k)
        {
            j = (i+k)/2; //Find the middle point
            //Continuously sort through the halves
            mergeSort(array, i, j);
            mergeSort(array, j+1, k);

            //Merge the halves in sorted order
            merge(array, i, j, k);
        }
    }
    public static void main(String[] args)
    {
        Scanner arrayMaker = new Scanner(System.in); //User input
        ArrayList<Integer> unsortedList = new ArrayList<Integer>(); //ArrayList for making an array
        String parseThis; //String for use in loop
        int[] sortedArray;

        System.out.print("Input an integer, or press Enter to send the array to the sorter: "); //First prompt for the user to input a number
        parseThis = arrayMaker.nextLine(); //Make a String out of user input
        unsortedList.add(Integer.parseInt(parseThis)); //Add inputted integer into an ArrayList
        do //Do the loop until the next input is empty
        {
            System.out.print("Input an integer, or press Enter to send the array to the sorter: ");
            parseThis = arrayMaker.nextLine();
            if(!parseThis.isEmpty())
            {
                unsortedList.add(Integer.parseInt(parseThis));
            }
        }while(!arrayMaker.nextLine().isEmpty());
        for(int i = 0; i < unsortedList.size(); i++)
        {
            System.out.print(unsortedList.get(i) + " "); //Print unsorted array. It's technically an ArrayList right now, but this will fill the array to send to the sorting method.
        }
        int[] array = new int[unsortedList.size()]; //Make new array with matching size to the ArrayList
        for(int i = 0; i < array.length; i++)
        {
            array[i] = unsortedList.get(i); //Clone the ArrayList to the array of ints
        }
        mergeSort(array, 0, array.length - 1); //Send the array to be sorted

    }
}

```
