## How to rotate a matrix?

1. Find transpose
2. Invert the Matrix

#### Q1. Determine Whether Matrix Can Be Obtained By Rotation

https://leetcode.com/problems/determine-whether-matrix-can-be-obtained-by-rotation/description/

##### Note: It the Matrix is of size N*M, rotate and compare (N\*M)-1 times. Don't forget to compare with the original matrix initially.

    class Solution {
    public boolean findRotation(int[][] mat, int[][] target) {
        boolean isEqual=false;
        int rotations = mat.length * mat[0].length;

        isEqual = compare(mat,target);

        for(int i=0;i<rotations;i++){
            if(!isEqual){
                mat = transpose(mat);
                mat= invert(mat);
            }
            isEqual = compare(mat,target);
        }

        return isEqual;
    }
    public int[][] transpose(int[][] mat){
        int result[][] = new int[mat.length][mat[0].length];
        for(int i=0;i<mat.length;i++){
            for(int j=0;j<mat[i].length;j++){
                result[i][j] = mat[j][i];
            }
        }
        return result;
    }

    public int[][] invert(int[][] mat){
        int result[][] = new int[mat.length][mat[0].length];
        for(int i=0;i<mat.length;i++){
            for(int j=mat[i].length-1;j>=0;j--){
                result[i][mat[i].length-1-j] = mat[i][j];
            }
        }
        return result;
    }

    public boolean compare(int[][] mat, int[][] target){
        for(int i=0;i<mat.length;i++){
            for(int j=0;j<mat[i].length;j++){
                if(mat[i][j]!=target[i][j])
                    return false;
            }
        }
        return true;
    }
    }
