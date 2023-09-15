---
layout: project
type: project
image: img/Sudoku.png
title: "Sukdoku Cheats(Free)(No virus)(2024)"
date: 2023
published: true
labels:
  - Java
summary: "A sudoku puzzle solver."
---
This program takes in Sudoku puzzles in the form of multidimensional arrays. These arrays are sent to a method called checkSudoku that takes in a multidimensional array and analyzes them to ensure that they are in accordance with Sudoku's rules.

-------------------------------------------------------------------------------------------------------
	  public static boolean checkSudoku (int [] [] sudoku, boolean printErrors)
	  {
	    if (sudoku.length != 9) {
	      if (printErrors) {
	        System.out.println ("sudoku has " + sudoku.length +
	                            " rows, should have 9");
	      }
	      return false;
	    }
	    for (int i = 0; i < sudoku.length; i++) {
	      if (sudoku [i].length != 9) {
	        if (printErrors) {
	          System.out.println ("sudoku row " + i + " has " +
	                              sudoku [i].length + " cells, should have 9");
	        }
	        return false;
	      }
	    }
	    /* check each cell for conflicts */
	    for (int i = 0; i < sudoku.length; i++) {
	      for (int j = 0; j < sudoku.length; j++) {
	        int cell = sudoku [i] [j];
	        if (cell == 0) {
	          continue;   /* blanks are always OK */
	        }
	        if ((cell < 1) || (cell > 9)) {
	          if (printErrors) {
	            System.out.println ("sudoku row " + i + " column " + j +
	                                " has illegal value " + cell);
	          }
	          return false;
	        }
	        /* does it match any other value in the same row? */
	        for (int m = 0; m < sudoku.length; m++) {
	          if ((j != m) && (cell == sudoku [i] [m])) {
	            if (printErrors) {
	              System.out.println ("sudoku row " + i + " has " + cell +
	                                  " at both positions " + j + " and " + m);
	            }
	            return false;
	          }
	        }
	        /* does it match any other value it in the same column? */
	        for (int k = 0; k < sudoku.length; k++) {
	          if ((i != k) && (cell == sudoku [k] [j])) {
	            if (printErrors) {
	              System.out.println ("sudoku column " + j + " has " + cell +
	                                  " at both positions " + i + " and " + k);
	            }
	            return false;
	          }
	        }
	        /* does it match any other value in the 3x3? */
	        for (int k = 0; k < 3; k++) {
	          for (int m = 0; m < 3; m++) {
	            int testRow = (i / 3 * 3) + k;   /* test this row */
	            int testCol = (j / 3 * 3) + m;   /* test this col */
	            if ((i != testRow) && (j != testCol) &&
	                (cell == sudoku [testRow] [testCol])) {
	              if (printErrors) {
	                System.out.println ("sudoku character " + cell + " at row " +
	                                    i + ", column " + j + 
	                                    " matches character at row " + testRow +
	                                    ", column " + testCol);
	              }
	              return false;
	            }
	          }
	        }
	      }
	    }
	    return true;
	  }






After checking the array, it is passed to another method called fillSudoku, which fills in the array according to Sudoku's rules. To ensure that the Sudoku puzzle is solved correctly, the checkSudoku method is called within the fillSudoku metho.  


-------------------------------------------------------------------------------------------------------
 public static boolean fillSudoku (int [] [] sudoku) {
		boolean allFilled = true;
		int row = -1;
		int col = -1;
		
		for(int i = 0; i < 9; i++) {
			for(int j = 0; j < 9; j++) {
				if(sudoku[i][j] == 0 ) {
					row = i;
					col = j;
					allFilled = false;
					break;
				}
			}
			if(!allFilled) {
				break;
			}
		}
		if(allFilled) {
			return true;
		}
		for(int num = 1; num <=9; num++) {
			sudoku[row][col] = num;
			if(checkSudoku(sudoku,false)) {
				if(fillSudoku(sudoku)) {
					return true;
				}
			}
			
		}
		sudoku[row][col] = 0;
	    return false;
	  }
	}






In order to test these functions, a separate file was created to assess the capability of my program. This file contains a method named 'testSudoku' that prints the unsolved puzzle and its solution. If there are any mistakes or incompletions made by the program, or if an invalid puzzle was submitted, the 'testSudoku' method will display them.

-------------------------------------------------------------------------------------------------------
	  private static void testSudoku(String name,
	                                 int [] [] sudoku, int [] [] solution)
	  {
	    System.out.println ("solving " + name + "\n" +
	                        Sudoku.toString (sudoku, true));
	    if (Sudoku.fillSudoku (sudoku)) {
	      if (isFilled(sudoku) && Sudoku.checkSudoku (sudoku, true)) {
	        System.out.println ("success!\n" + Sudoku.toString (sudoku, true));
	        if (solution != null) {
	          int [] [] diff = sameSudoku (sudoku, solution);
	          if (diff != null) {
	            System.out.println ("given solution:\n" +
	                                Sudoku.toString (solution, true));
	            System.out.println ("difference between solutions:\n" +
	                                Sudoku.toString (diff, true));
	          }
	        }
	      } else {   /* the supposed solution is not a complete or valid sudoku */
	        if (! isFilled(sudoku)) {
	          System.out.println ("sudoku was not completely filled:\n" +
	                              Sudoku.toString (sudoku, false));
	        }
	        if (! Sudoku.checkSudoku(sudoku, false)) {
	          System.out.println ("sudoku is not a valid solution:\n" +
	                              Sudoku.toString (sudoku, false));
	        }
	      }
	    } else {
	      System.out.println ("unable to complete sudoku " + name + "\n" +
	                          Sudoku.toString (sudoku, true));
	    }
	  }
