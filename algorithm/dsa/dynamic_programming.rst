Dynamic Programming 
===================

Longest Common Subsequence 
--------------------------

:Time Complexity: :math:`O(N\times M)`
:Auxiliary Space: :math:`O(N\times M)`

.. tabs::

    .. code-tab:: python

        def lcs(X, Y):
            n = len(X)
            m = len(Y)
            dp = [[0 for j in range(m+1)] for i in range(n+1)]
            for i in range(1, n+1):
                for j in range(1, m+1):
                    if X[i-1] == Y[j-1]:
                        dp[i][j] = dp[i-1][j-1] + 1
                    else:
                        dp[i][j] = max(dp[i-1][j], dp[i][j-1])
            return dp[n][m]

        if __name__ == '__main__':
            X = "AGGTAB"
            Y = "GXTXAYB"
            print(lcs(X, Y))

    .. code-tab:: cpp

        #include <bits/stdc++.h>
        using namespace std;

        int lcs(string X, string Y) {
            int n = X.length();
            int m = Y.length();
            int dp[n+1][m+1] = {};
            for (int i=1; i<=n; ++i) {
                for (int j=1; j<=m; ++j) {
                    if (X[i-1] == Y[j-1]) {
                        dp[i][j] = dp[i-1][j-1] + 1;
                    } else {
                        dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
                    }
                }
            }
            return dp[n][m];
        }

        int main() {
            string X = "AGGTAB";
            string Y = "GXTXAYB";
            cout << lcs(X, Y);
        }

    .. code-tab:: java

        class LCS {
            static int lcs(String X, String Y) {
                int n = X.length();
                int m = Y.length();
                int dp[][] = new int[n+1][m+1];
                for (int i=1; i<=n; ++i) {
                    for (int j=1; j<=m; ++j) {
                        if (X.charAt(i-1) == Y.charAt(j-1)) {
                            dp[i][j] = dp[i-1][j-1] + 1;
                        } else {
                            dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
                        }
                    }
                }
                return dp[n][m];
            }
            public static void main(String args[]) {
                String X = "AGGTAB";
                String Y = "GXTXAYB";
                System.out.println(lcs(X, Y));
            }
        }

Longest Increasing Subsequence 
------------------------------

:Time Complexity: :math:`O(N^2)`
:Auxiliary Space: :math:`O(N)`

.. tabs::

    .. code-tab:: python

        def lis(arr):
            n = len(arr)
            dp = [1 for i in range(n)]
            for i in range(1, n):
                for j in range(0, i):
                    if arr[j] < arr[i] and dp[j]+1 > dp[i]:
                        dp[i] = dp[j] + 1
            maxL = 1
            for d in dp:
                maxL = max(maxL, d)
            return maxL

        if __name__ == '__main__':
            arr = [10, 22, 9, 33, 21, 50, 41, 60]
            print(lis(arr))

    .. code-tab:: cpp

        #include <bits/stdc++.h>
        using namespace std;

        int lis(vector<int> arr) {
            int n = arr.size();
            int dp[n] = {};
            for (int i=0; i<n; ++i) {
                dp[i] = 1;
            }
            for (int i=1; i<n; ++i) {
                for (int j=0; j<i; ++j) {
                    if (arr[j]<arr[i] && dp[j]+1>dp[i]) {
                        dp[i] = dp[j] + 1;
                    }
                }
            }
            int maxL = 1;
            for (int i=0; i<n; ++i) {
                if (dp[i] > maxL) {
                    maxL = dp[i];
                }
            }
            return maxL;
        }

        int main() {
            vector<int> arr{10, 22, 9, 33, 21, 50, 41, 60};
            cout << lis(arr);
        }

    .. code-tab:: java

        class LIS {
            static int lis(int arr[]) {
                int n = arr.length;
                int dp[] = new int[n];
                for (int i=0; i<n; ++i) {
                    dp[i] = 1;
                }
                for (int i=1; i<n; ++i) {
                    for (int j=0; j<i; ++j) {
                        if (arr[j]<arr[i] && dp[j]+1>dp[i]) {
                            dp[i] = dp[j] + 1;
                        }
                    }
                }
                int maxL = 1;
                for (int i=0; i<n; ++i) {
                    if (dp[i] > maxL) {
                        maxL = dp[i];
                    }
                }
                return maxL;
            }
            public static void main(String args[]) {
                int arr[] = {10, 22, 9, 33, 21, 50, 41, 60};
                System.out.println(lis(arr));
            }
        }

Edit Distance
-------------

:Time Complexity: :math:`O(N\times M)`
:Auxiliary Space: :math:`O(N\times M)`

.. tabs::

    .. code-tab:: python

        def ed(X, Y):
            n = len(X)
            m = len(Y)
            dp = [[0 for j in range(m+1)] for i in range(n+1)]
            for i in range(n+1):
                dp[i][0] = i
            for j in range(m+1):
                dp[0][j] = j
            for i in range(1, n+1):
                for j in range(1, m+1):
                    if X[i-1] == Y[j-1]:
                        dp[i][j] = dp[i-1][j-1]
                    else:
                        dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1
            return dp[n][m]

        if __name__ == '__main__':
            X = "sunday"
            Y = "saturday"
            print(ed(X, Y))

    .. code-tab:: cpp

        #include <bits/stdc++.h>
        using namespace std;

        int min(int x, int y, int z) {
            return min(x, min(y, z));
        }

        int ed(string X, string Y) {
            int n = X.length();
            int m = Y.length();
            int dp[n+1][m+1] = {};
            for (int i=0; i<=n; ++i) {
                dp[i][0] = i;
            }
            for (int j=0; j<=m; ++j) {
                dp[0][j] = j;
            }
            for (int i=1; i<=n; ++i) {
                for (int j=1; j<=m; ++j) {
                    if (X[i-1]==Y[j-1]) {
                        dp[i][j] = dp[i-1][j-1];
                    } else {
                        dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1;
                    }
                }
            }
            return dp[n][m];
        }

        int main() {
            string X = "sunday";
            string Y = "saturday";
            cout << ed(X, Y);
        }

    .. code-tab:: java

        class ED {
            static int min(int x, int y, int z) {
                return Math.min(x, Math.min(y, z));
            }
            static int ed(String X, String Y) {
                int n = X.length();
                int m = Y.length();
                int dp[][] = new int[n+1][m+1];
                for (int i=0; i<=n; ++i) {
                    dp[i][0] = i;
                }
                for (int j=0; j<m; ++j) {
                    dp[0][j] = j;
                }
                for (int i=1; i<=n; ++i) {
                    for (int j=1; j<=m; ++j) {
                        if (X.charAt(i-1)==Y.charAt(j-1)) {
                            dp[i][j] = dp[i-1][j-1];
                        } else {
                            dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1;
                        }
                    }
                }
                return dp[n][m];
            }
            public static void main(String args[]) {
                String X = "sunday";
                String Y = "saturday";
                System.out.println(ed(X, Y));
            }
        }

Minimum Partition
-----------------

:Time Complexity: :math:`O(N\times S)`
:Auxiliary Space: :math:`O(N\times S)`

.. tabs::

    .. code-tab:: python

        def mp(arr):
            n = len(arr)
            s = sum(arr)
            dp = [[False for j in range(s+1)] for i in range(n+1)]
            for i in range(n+1):
                dp[i][0] = True
            for i in range(1, n+1):
                for j in range(1, s+1):
                    if arr[i-1] <= j:
                        dp[i][j] = dp[i-1][j] or dp[i-1][j-arr[i-1]]
                    else:
                        dp[i][j] = dp[i-1][j]
            m = s
            for j in range(s//2, -1, -1):
                if dp[n][j] == True:
                    m = s - 2 * j 
                    break
            return m
            
        if __name__ == '__main__':
            arr = [3, 1, 4, 2, 2, 1]
            print(mp(arr))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int mp(vector<int> arr) {
            int n = arr.size();
            int s = 0;
            for (int a : arr) {
                s += a;
            }
            bool dp[n+1][s+1] = {};
            for (int i=0; i<n+1; ++i) {
                for (int j=0; j<s+1; ++j) {
                    if (j == 0) {
                        dp[i][j] = true;
                    }
                }
            }
            for (int i=1; i<n+1; ++i) {
                for (int j=1; j<s+1; ++j) {
                    if (arr[i-1]<=j) {
                        dp[i][j] = dp[i-1][j] || dp[i-1][j-arr[i-1]];
                    } else {
                        dp[i][j] = dp[i-1][j];
                    }
                }
            }
            int m = s;
            for (int j=s/2; j>=0; --j) {
                if (dp[n][j] == true) {
                    m = s - 2 * j;
                    break;
                }
            }
            return m;
        }

        int main() {
            vector<int> arr{3, 1, 4, 2, 2, 1};
            cout << mp(arr);
        }

    .. code-tab:: java

        class MP {
            static int mp(int arr[]) {
                int n = arr.length;
                int s = 0;
                for (int a : arr) {
                    s += a;
                }
                boolean dp[][] = new boolean[n+1][s+1];
                for (int i=0; i<n+1; ++i) {
                    for (int j=0; j<s+1; ++j) {
                        if (j == 0) {
                            dp[i][j] = true;
                        }
                    }
                }
                for (int i=1; i<n+1; ++i) {
                    for (int j=1; j<s+1; ++j) {
                        if (arr[i-1] <= j) {
                            dp[i][j] = dp[i-1][j] || dp[i-1][j-arr[i-1]];
                        } else {
                            dp[i][j] = dp[i-1][j];
                        }
                    }
                }
                int m = s;
                for (int j=s/2; j>=0; --j) {
                    if (dp[n][j]==true) {
                        m = s - 2 * j;
                        break;
                    }
                }
                return m;
            }
            public static void main(String args[]) {
                int arr[] = {3, 1, 4, 2, 2, 1};
                System.out.println(mp(arr));
            }
        }

Ways to Cover a Distance
------------------------

:Time Complexity: :math:`O(N)`
:Auxiliary Space: :math:`O(N)`

.. tabs::

    .. code-tab:: python

        def wcd(n):
            dp = [0 for i in range(n+1)]
            dp[0] = 1
            if n >= 1: dp[1] = 1
            if n >= 2: dp[2] = 2
            for i in range(3, n+1):
                dp[i] = dp[i-1] + dp[i-2] + dp[i-3]
            return dp[n]

        if __name__ == '__main__':
            print(wcd(4))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int wcd(int n) {
            int dp[n+1] = {};
            dp[0] = 1;
            if (n>=1) dp[1] = 1;
            if (n>=2) dp[2] = 2;
            for (int i=3; i<n+1; ++i) {
                dp[i] = dp[i-1] + dp[i-2] + dp[i-3];
            }
            return dp[n];
        }

        int main() {
            cout << wcd(4);
        }

    .. code-tab:: java

        class WCD {
            static int wcd(int n) {
                int dp[] = new int[n+1];
                dp[0] = 1;
                if (n>=1) dp[1] = 1;
                if (n>=2) dp[2] = 2;
                for (int i=3; i<n+1; ++i) {
                    dp[i] = dp[i-1] + dp[i-2] + dp[i-3];
                }
                return dp[n];
            }
            public static void main(String args[]) {
                System.out.println(wcd(4));
            }
        }

Longest Path In Matrix
----------------------

:Time Complexity: :math:`O(N\times M)`
:Auxiliary Space: :math:`O(N\times M)`

.. tabs::

    .. code-tab:: python

        def search(i, j, mat, dp):
            if i<0 or i>len(mat) or j<0 or j>len(mat[0]): return 0
            if dp[i][j] != -1: return dp[i][j]
            x, y, z, w = 1, 1, 1, 1
            if i>0 and mat[i-1][j]==mat[i][j]+1:
                x = 1 + search(i-1, j, mat, dp)
            if i<len(mat)-1 and mat[i+1][j]==mat[i][j]+1:
                y = 1 + search(i+1, j, mat, dp)
            if j>0 and mat[i][j-1]==mat[i][j]+1:
                z = 1 + search(i, j-1, mat, dp)
            if j<len(mat[0])-1 and mat[i][j+1]==mat[i][j]+1:
                w = 1 + search(i, j+1, mat, dp)
            dp[i][j] = max(x, y, z, w)
            return dp[i][j]

        def lpim(mat):
            n = len(mat)
            m = len(mat[0])
            dp = [[-1 for j in range(m)] for i in range(n)]
            maxL = 1
            for i in range(n):
                for j in range(m):
                    maxL = max(maxL, search(i, j, mat, dp))
            return maxL

        if __name__ == '__main__':
            mat = [[1, 2, 9],
                [5, 3, 8],
                [4, 6, 7]]
            print(lpim(mat))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int search(int i, int j, vector<vector<int>> mat, vector<vector<int>> dp) {
            if (i<0 || i>mat.size() || j<0 || j>mat[0].size()) {
                return 0;
            }
            if (dp[i][j] != -1) {
                return dp[i][j];
            }
            int x=1, y=1, z=1, w=1;
            if (i>0 && mat[i-1][j]==mat[i][j]+1) {
                x = 1 + search(i-1, j, mat, dp);
            }
            if (i<mat.size()-1 && mat[i+1][j]==mat[i][j]+1) {
                y = 1 + search(i+1, j, mat, dp);
            }
            if (j>0 && mat[i][j-1]==mat[i][j]+1) {
                z = 1 + search(i, j-1, mat, dp);
            }
            if (j<mat[0].size()-1 && mat[i][j+1]==mat[i][j]+1) {
                w = 1 + search(i, j+1, mat, dp);
            }
            dp[i][j] = max(x, max(y, max(z, w)));
            return dp[i][j];
        }

        int lpim(vector<vector<int>> mat) {
            int n = mat.size();
            int m = mat[0].size();
            vector<vector<int>> dp(n, vector<int> (m, -1));
            int maxL = 1;
            for (int i=0; i<n; ++i) {
                for (int j=0; j<m; ++j) {
                    maxL = max(maxL, search(i, j, mat, dp));
                }
            }
            return maxL;
        }

        int main() {
            vector<vector<int>> mat{{1, 2, 9}, {5, 3, 8}, {4, 6, 7}};
            cout << lpim(mat);
        }

    .. code-tab:: java

        class LPIM {
            static int search(int i, int j, int mat[][], int dp[][]) {
                if (i<0 || i>mat.length || j<0 || j>mat[0].length) {
                    return 0;
                }
                if (dp[i][j] != -1) {
                    return dp[i][j];
                }
                int x=1, y=1, z=1, w=1;
                if (i>0 && mat[i-1][j]==mat[i][j]+1) {
                    x = 1 + search(i-1, j, mat, dp);
                }
                if (i<mat.length-1 && mat[i+1][j]==mat[i][j]+1) {
                    y = 1 + search(i+1, j, mat, dp);
                }
                if (j>0 && mat[i][j-1]==mat[i][j]+1) {
                    z = 1 + search(i, j-1, mat, dp);
                }
                if (j<mat[0].length-1 && mat[i][j+1]==mat[i][j]+1) {
                    w = 1 + search(i, j+1, mat, dp);
                }
                dp[i][j] = Math.max(x, Math.max(y, Math.max(z, w)));
                return dp[i][j];
            }
            static int lpim(int mat[][]) {
                int n = mat.length;
                int m = mat[0].length;
                int dp[][] = new int[n][m];
                for (int i=0; i<n; ++i) {
                    for (int j=0; j<m; ++j) {
                        dp[i][j] = -1;
                    }
                }
                int maxL = 1;
                for (int i=0; i<n; ++i) {
                    for (int j=0; j<m; ++j) {
                        maxL = Math.max(maxL, search(i, j, mat, dp));
                    }
                }
                return maxL;
            }
            public static void main(String args[]) {
                int mat[][] = {{1, 2, 9}, {5, 3, 8}, {4, 6, 7}};
                System.out.println(lpim(mat));
            }
        }

Subset Sum Problem
------------------

:Time Complexity: :math:`O(N\times S)`
:Auxiliary Space: :math:`O(N\times S)`

.. tabs::

    .. code-tab:: python

        def sss(_set, _sum):
            n = len(_set)
            s = _sum
            dp = [[False for j in range(s+1)] for i in range(n+1)]
            for i in range(n+1):
                dp[i][0] = True
            for i in range(1, n+1):
                for j in range(1, s+1):
                    if _set[i-1] <= j:
                        dp[i][j] = dp[i-1][j] or dp[i-1][j-_set[i-1]]
                    else:
                        dp[i][j] = dp[i-1][j]
            return dp[n][s]

        if __name__ == '__main__':
            _set = [3, 34, 4, 12, 5, 2]
            _sum = 9
            print(sss(_set, _sum))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        bool sss(vector<int> _set, int _sum) {
            int n=_set.size();
            int s=_sum;
            bool dp[n+1][s+1] = {};
            for (int i=0; i<n+1; ++i) {
                dp[i][0] = true;
            }
            for (int i=1; i<n+1; ++i) {
                for (int j=1; j<s+1; ++j) {
                    if (_set[i-1]<=j) {
                        dp[i][j] = dp[i-1][j] || dp[i-1][j-_set[i-1]];
                    } else {
                        dp[i][j] = dp[i-1][j];
                    }
                }
            }
            return dp[n][s];
        }

        int main() {
            vector<int> _set{3, 34, 4, 12, 5, 2}; 
            int _sum = 9;
            cout << sss(_set, _sum);
        }

    .. code-tab:: java

        class SSS {
            static boolean sss(int _set[], int _sum) {
                int n=_set.length;
                int s=_sum;
                boolean dp[][] = new boolean[n+1][s+1];
                for (int i=0; i<n+1; ++i) {
                    dp[i][0] = true;
                }
                for (int i=1; i<n+1; ++i) {
                    for (int j=1; j<s+1; ++j) {
                        if (_set[i-1]<=j) {
                            dp[i][j] = dp[i-1][j] || dp[i-1][j-_set[i-1]];
                        } else {
                            dp[i][j] = dp[i-1][j];
                        }
                    }
                }
                return dp[n][s];
            }
            public static void main(String args[]) {
                int _set[] = {3, 34, 4, 12, 5, 2};
                int _sum = 9;
                System.out.println(sss(_set, _sum));
            }
        }

Optimal Strategy for a Game
---------------------------

:Time Complexity: :math:`O(N^2)`
:Auxiliary Space: :math:`O(N^2)`

.. tabs::

    .. code-tab:: python

        def osg(arr):
            n = len(arr)
            dp = [[0 for j in range(n)] for i in range(n)]
            for j in range(n):
                i = j
                dp[i][j] = arr[i]
            for j in range(1, n):
                i = j - 1
                dp[i][j] = max(arr[i], arr[j])
            for g in range(2, n):
                for j in range(g, n):
                    i = j - g
                    dp[i][j] = max(arr[i]+min(dp[i+2][j], dp[i+1][j-1]), arr[j]+min(dp[i+1][j-1], dp[i][j-2]))
            return dp[0][n-1]

        if __name__ == '__main__':
            arr1 = [8, 15, 3, 7]
            print(osg(arr1))
            arr2 = [2, 2, 2, 2]
            print(osg(arr2))
            arr3 = [20, 30, 2, 2, 2, 10]
            print(osg(arr3))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int osg(vector<int> arr) {
            int n = arr.size();
            int dp[n][n];
            int i;
            for (int j=0; j<n; ++j) {
                i = j;
                dp[i][j] = arr[i];
            }
            for (int j=1; j<n; ++j) {
                i = j - 1;
                dp[i][j] = max(arr[i], arr[j]);
            }
            for (int g=2; g<n; ++g) {
                for (int j=g; j<n; ++j) {
                    i = j - g;
                    dp[i][j] = max(arr[i]+min(dp[i+2][j], dp[i+1][j-1]), arr[j]+min(dp[i+1][j-1], dp[i][j-2]));
                }
            }
            return dp[0][n-1];
        }

        int main() {
            vector<int> arr1{8, 15, 3, 7};
            cout << osg(arr1) << endl;
            vector<int> arr2{2, 2, 2, 2};
            cout << osg(arr2) << endl;
            vector<int> arr3{20, 30, 2, 2, 2, 10};
            cout << osg(arr3) << endl;
        }

    .. code-tab:: java

        class OSG {
            static int osg(int arr[]) {
                int n = arr.length;
                int dp[][] = new int[n][n];
                int i;
                for (int j=0; j<n; ++j) {
                    i = j;
                    dp[i][j] = arr[i];
                }
                for (int j=1; j<n; ++j) {
                    i = j - 1;
                    dp[i][j] = Math.max(arr[i], arr[j]);
                }
                for (int g=2; g<n; ++g) {
                    for (int j=g; j<n; ++j) {
                        i = j - g;
                        dp[i][j] = Math.max(arr[i]+Math.min(dp[i+2][j], dp[i+1][j-1]), arr[j]+Math.min(dp[i+1][j-1], dp[i][j-2]));
                    }
                }
                return dp[0][n-1];
            }
            public static void main(String args[]) {
                int arr1[] = {8, 15, 3, 7};
                System.out.println(osg(arr1));
                int arr2[] = {2, 2, 2, 2};
                System.out.println(osg(arr2));
                int arr3[] = {20, 30, 2, 2, 2, 10};
                System.out.println(osg(arr3));
            }
        }

0-1 Knapsack Problem 
--------------------

:Time Complexity: :math:`O(N\times W)`
:Auxiliary Space: :math:`O(N\times W)`

.. tabs::

    .. code-tab:: python

        def kp01(val, wt, w):
            n = len(val)
            dp = [[0 for j in range(w+1)] for i in range(n+1)]
            for i in range(1, n+1):
                for j in range(1, w+1):
                    if wt[i-1] <= j:
                        dp[i][j] = max(dp[i-1][j], val[i-1]+dp[i-1][j-wt[i-1]])
                    else:
                        dp[i][j] = dp[i-1][j]
            return dp[n][w]

        if __name__ == '__main__':
            val = [60, 100, 120]
            wt = [10, 20, 30]
            w = 50
            print(kp01(val, wt, w))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int kp01(vector<int> val, vector<int> wt, int w) {
            int n = val.size();
            int dp[n+1][w+1] = {};
            for (int i=1; i<=n; ++i) {
                for (int j=1; j<=w; ++j) {
                    if  (wt[i-1]<=j) {
                        dp[i][j] = max(dp[i-1][j], val[i-1]+dp[i-1][j-wt[i-1]]);
                    } else {
                        dp[i][j] = dp[i-1][j];
                    }
                }
            }
            return dp[n][w];
        }

        int main() {
            vector<int> val{60, 100, 120};
            vector<int> wt{10, 20, 30};
            int w = 50;
            cout << kp01(val, wt, w);
        }

    .. code-tab:: java

        class KP01 {
            static int kp01(int val[], int wt[], int w) {
                int n = val.length;
                int dp[][] = new int[n+1][w+1];
                for (int i=1; i<=n; ++i) {
                    for (int j=1; j<=w; ++j) {
                        if (wt[i-1]<=j) {
                            dp[i][j] = Math.max(dp[i-1][j], val[i-1]+dp[i-1][j-wt[i-1]]);
                        } else {
                            dp[i][j] = dp[i-1][j];
                        }
                    }
                }
                return dp[n][w];
            }
            public static void main(String args[]) {
                int val[] = {60, 100, 120};
                int wt[] = {10, 20, 30};
                int w = 50;
                System.out.println(kp01(val, wt, w));
            }
        }

Boolean Parenthesization Problem
--------------------------------

:Time Complexity: :math:`O(N^3)`
:Auxiliary Space: :math:`O(N^2)`

.. tabs::

    .. code-tab:: python

        def bpp(symb, oper):
            n = len(symb)
            T = [[0 for j in range(n)] for i in range(n)]
            F = [[0 for j in range(n)] for i in range(n)]
            for i in range(n):
                if symb[i] == 'T':
                    T[i][i] = 1
                    F[i][i] = 0
                elif symb[i] == 'F':
                    T[i][i] = 0
                    F[i][i] = 1
            for g in range(1, n):
                for j in range(g, n):
                    i = j - g
                    for k in range(i, j):
                        if oper[k] == '&':
                            T[i][j] += T[i][k] * T[k+1][j]
                            F[i][j] += F[i][k] * F[k+1][j] + F[i][k] * T[k+1][j] + T[i][k] * F[k+1][j]
                        elif oper[k] == '|':
                            T[i][j] += F[i][k] * T[k+1][j] + T[i][k] * F[k+1][j] + T[i][k] * T[k+1][j]
                            F[i][j] += F[i][k] * F[k+1][j]
                        elif oper[k] == '^':
                            T[i][j] += F[i][k] * T[k+1][j] + T[i][k] * F[k+1][j]
                            F[i][j] += F[i][k] * F[k+1][j] + T[i][k] * T[k+1][j]
            return T[0][n-1]

        if __name__ == '__main__':
            symb = "TTFT"
            oper = "|&^"
            print(bpp(symb, oper))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int bpp(string symb, string oper) {
            int n = symb.length();
            int T[n][n] = {};
            int F[n][n] = {};
            for (int i=0; i<n; ++i) {
                if (symb[i] == 'T') {
                    T[i][i] = 1;
                    F[i][i] = 0;
                } else if (symb[i] == 'F') {
                    T[i][i] = 0;
                    F[i][i] = 1;
                }
            }
            for (int g=1; g<n; ++g) {
                for (int j=g; j<n; ++j) {
                    int i = j - g;
                    for (int k=i; k<j; ++k) {
                        if (oper[k] == '&') {
                            T[i][j] += T[i][k] * T[k+1][j];
                            F[i][j] += F[i][k] * F[k+1][j] + F[i][k] * T[k+1][j] + T[i][k] * F[k+1][j];
                        } else if (oper[k] == '|') {
                            T[i][j] += F[i][k] * T[k+1][j] + T[i][k] * F[k+1][j] + T[i][k] * T[k+1][j];
                            F[i][j] += F[i][k] * F[k+1][j];
                        } else if (oper[k] == '^') {
                            T[i][j] += F[i][k] * T[k+1][j] + T[i][k] * F[k+1][j];
                            F[i][j] += F[i][k] * F[k+1][j] + T[i][k] * T[k+1][j];
                        }
                    }
                }
            }
            return T[0][n-1];
        }

        int main() {
            string symb = "TTFT";
            string oper = "|&^";
            cout << bpp(symb, oper);
        }

    .. code-tab:: java

        class BPP {
            static int bpp(String symb, String oper) {
                int n = symb.length();
                int T[][] = new int[n][n];
                int F[][] = new int[n][n];
                for (int i=0; i<n; ++i) {
                    if (symb.charAt(i) == 'T') {
                        T[i][i] = 1;
                        F[i][i] = 0;
                    } else if (symb.charAt(i) == 'F') {
                        T[i][i] = 0;
                        F[i][i] = 1;
                    }
                }
                for (int g=1; g<n; ++g) {
                    for (int j=g; j<n; ++j) {
                        int i = j - g;
                        for (int k=i; k<j; ++k) {
                            if (oper.charAt(k) == '&') {
                                T[i][j] += T[i][k] * T[k+1][j];
                                F[i][j] += F[i][k] * F[k+1][j] + F[i][k] * T[k+1][j] + T[i][k] * F[k+1][j];
                            } else if (oper.charAt(k) == '|'){
                                T[i][j] += F[i][k] * T[k+1][j] + T[i][k] * F[k+1][j] + T[i][k] * T[k+1][j];
                                F[i][j] += F[i][k] * F[k+1][j];
                            } else if (oper.charAt(k) == '^') {
                                T[i][j] += F[i][k] * T[k+1][j] + T[i][k] * F[k+1][j];
                                F[i][k] += F[i][k] * F[k+1][j] + T[i][k] * T[k+1][j];
                            }
                        }
                    }
                }
                return T[0][n-1];
            }
            public static void main(String args[]) {
                String symb = "TTFT";;
                String oper = "|&^";
                System.out.println(bpp(symb, oper));
            }
        }

Shortest Common Supersequence
-----------------------------

:Time Complexity: :math:`O(N\times M)`
:Auxiliary Space: :math:`O(N\times M)`

.. tabs::

    .. code-tab:: python

        def scs(X, Y):
            n = len(X)
            m = len(Y)
            dp = [[0 for j in range(m+1)] for i in range(n+1)]
            for i in range(1, n+1):
                dp[i][0] = i
            for j in range(1, m+1):
                dp[0][j] = j
            for i in range(1, n+1):
                for j in range(1, m+1):
                    if X[i-1] == Y[j-1]:
                        dp[i][j] = dp[i-1][j-1] + 1
                    else:
                        dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + 1
            return dp[n][m]

        if __name__ == '__main__':
            X = "AGGTAB"
            Y = "GXTXAYB"
            print(scs(X, Y))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int scs(string X, string Y) {
            int n = X.length();
            int m = Y.length();
            int dp[n+1][m+1] = {};
            for (int i=1; i<=n; ++i) {
                dp[i][0] = i;
            }
            for (int j=1; j<=m; ++j) {
                dp[0][j] = j;
            }
            for (int i=1; i<=n; ++i) {
                for (int j=1; j<=m; ++j) {
                    if (X[i-1] == Y[j-1]) {
                        dp[i][j] = dp[i-1][j-1] + 1;
                    } else {
                        dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + 1;
                    }
                }
            }
            return dp[n][m];
        }

        int main() {
            string X = "AGGTAB";
            string Y = "GXTXAYB";
            cout << scs(X, Y);
        }

    .. code-tab:: java

        class SCS {
            static int scs(String X, String Y) {
                int n = X.length();
                int m = Y.length();
                int dp[][] = new int[n+1][m+1];
                for (int i=1; i<=n; ++i) {
                    dp[i][0] = i;
                }
                for (int j=1; j<=m; ++j) {
                    dp[0][j] = j;
                }
                for (int i=1; i<=n; ++i) {
                    for (int j=1; j<=m; ++j) {
                        if (X.charAt(i-1) == Y.charAt(j-1)) {
                            dp[i][j] = dp[i-1][j-1] + 1;
                        } else {
                            dp[i][j] = Math.min(dp[i-1][j], dp[i][j-1]) + 1;
                        }
                    }
                }
                return dp[n][m];
            }
            public static void main(String args[]) {
                String X = "AGGTAB";
                String Y = "GXTXAYB";
                System.out.println(scs(X, Y));
            }
        }

Matrix Chain Multiplication
---------------------------

:Time Complexity: :math:`O(N^3)`
:Auxiliary Space: :math:`O(N^2)`

.. tabs::

    .. code-tab:: python

        def mcm(arr):
            n = len(arr) - 1
            dp = [[0 for j in range(n)] for i in range(n)]
            for g in range(1, n):
                for j in range(g, n):
                    i = j - g
                    dp[i][j] = float('inf')
                    for k in range(i, j):
                        dp[i][j] = min(dp[i][j], dp[i][k] + dp[k+1][j] + arr[i] * arr[k+1] * arr[j+1])
            return dp[0][n-1]

        if __name__ == '__main__':
            arr = [1, 2, 3, 4]
            print(mcm(arr))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int mcm(vector<int> arr) {
            int n = arr.size() - 1;
            int dp[n][n] = {};
            for (int g=1; g<n; ++g) {
                for (int j=g; j<n; ++j) {
                    int i = j - g;
                    dp[i][j] = INT_MAX;
                    for (int k=i; k<j; ++k) {
                        dp[i][j] = min(dp[i][j], dp[i][k] + dp[k+1][j] + arr[i] * arr[k+1] * arr[j+1]);
                    }
                }
            }
            return dp[0][n-1];
        }

        int main() {
            vector<int> arr{1, 2, 3, 4};
            cout << mcm(arr);
        }

    .. code-tab:: java

        class MCM {
            static int mcm(int arr[]) {
                int n = arr.length - 1;
                int dp[][] = new int[n][n];
                for (int g=1; g<n; ++g) {
                    for (int j=g; j<n; ++j) {
                        int i = j - g;
                        dp[i][j] = Integer.MAX_VALUE;
                        for (int k=i; k<j; ++k) {
                            dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k+1][j] + arr[i] * arr[k+1] * arr[j+1]);
                        }
                    }
                }
                return dp[0][n-1];
            }
            public static void main(String args[]) {
                int arr[] = {1, 2, 3, 4};
                System.out.println(mcm(arr));
            }
        }

Partition Problem
-----------------

:Time Complexity: :math:`O(N\times S)`
:Auxiliary Space: :math:`O(N\times S)`

.. tabs::

    .. code-tab:: python

        def pp(arr):
            n = len(arr)
            s = sum(arr)
            if s % 2 == 1:
                return False
            dp = [[False for j in range(s//2+1)] for i in range(n+1)]
            for i in range(n+1):
                dp[i][0] = True
            for i in range(1, n+1):
                for j in range(1, s//2+1):
                    if arr[i-1] <= j:
                        dp[i][j] = dp[i-1][j] or dp[i-1][j-arr[i-1]]
                    else:
                        dp[i][j] = dp[i-1][j]
            return dp[n][s//2]

        if __name__ == '__main__':
            arr = [3, 1, 1, 2, 2, 1]
            print(pp(arr))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int pp(vector<int> arr) {
            int n = arr.size();
            int s = 0;
            for (int a : arr) {
                s += a;
            }
            if (s % 2 == 1) {
                return false;
            }
            bool dp[n+1][s/2+1] = {};
            for (int i=0; i<=n; ++i) {
                dp[i][0] = true;
            }
            for (int i=1; i<=n; ++i) {
                for (int j=1; j<=s/2; ++j) {
                    if (arr[i-1] <= j) {
                        dp[i][j] = dp[i-1][j] || dp[i-1][j-arr[i-1]];
                    } else {
                        dp[i][j] = dp[i-1][j];
                    }
                }
            }
            return dp[n][s/2];
        }

        int main() {
            vector<int> arr{3, 1, 1, 2, 2, 1};
            cout << pp(arr);
        }

    .. code-tab:: java

        class PP {
            static boolean pp(int arr[]) {
                int n = arr.length;
                int s = 0;
                for (int a : arr) {
                    s += a;
                }
                if (s % 2 == 1) {
                    return false;
                }
                boolean dp[][] = new boolean[n+1][s/2+1];
                for (int i=0; i<=n; ++i) {
                    dp[i][0] = true;
                }
                for (int i=1; i<=n; ++i) {
                    for (int j=1; j<=s/2; ++j) {
                        if (arr[i-1] <= j) {
                            dp[i][j] = dp[i-1][j] || dp[i-1][j-arr[i-1]];
                        } else {
                            dp[i][j] = dp[i-1][j];
                        }
                    }
                }
                return dp[n][s/2];
            }
            public static void main(String args[]) {
                int arr[] = {3, 1, 1, 2, 2, 1};
                System.out.println(pp(arr));
            }
        }

Rod Cutting
-----------

:Time Complexity: :math:`O(N^2)`
:Auxiliary Space: :math:`O(N^2)`

.. tabs::

    .. code-tab:: python

        def rc(price):
            n = len(price)
            dp = [[0 for j in range(n+1)] for i in range(n+1)]
            for i in range(1, n+1):
                for j in range(1, n+1):
                    if i <= j:
                        dp[i][j] = max(dp[i-1][j], dp[i-1][j-i] + price[i-1])
                    else:
                        dp[i][j] = dp[i-1][j]
            return dp[n][n]

        if __name__ == '__main__':
            price = [1, 5, 8, 9, 10, 17, 17, 20]
            print(rc(price))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int rc(vector<int> price) {
            int n = price.size();
            int dp[n+1][n+1] = {};
            for (int i=1; i<=n; ++i) {
                for (int j=1; j<=n; ++j) {
                    if (i <= j) {
                        dp[i][j] = max(dp[i-1][j], dp[i-1][j-i] + price[i-1]);
                    } else {
                        dp[i][j] = dp[i-1][j];
                    }
                }
            }
            return dp[n][n];
        }

        int main() {
            vector<int> price{1, 5, 8, 9, 10, 17, 17, 20};
            cout << rc(price);
        }

    .. code-tab:: java

        class RC {
            static int rc(int price[]) {
                int n = price.length;
                int dp[][] = new int[n+1][n+1];
                for (int i=1; i<=n; ++i) {
                    for (int j=1; j<=n; ++j) {
                        if (i <= j) {
                            dp[i][j] = Math.max(dp[i-1][j], dp[i-1][j-i] + price[i-1]);
                        } else {
                            dp[i][j] = dp[i-1][j];
                        }
                    }
                }
                return dp[n][n];
            }
            public static void main(String args[]) {
                int price[] = {1, 5, 8, 9, 10, 17, 17, 20};
                System.out.println(rc(price));
            }
        }

Coin Change Proplem
-------------------

:Time Complexity: :math:`O(N\times S)`
:Auxiliary Space: :math:`O(N\times S)`

.. tabs::

    .. code-tab:: python

        def ccp(coin, _sum):
            n = len(coin)
            s = _sum
            dp = [[0 for j in range(s+1)] for i in range(n+1)]
            for i in range(1, n+1):
                dp[i][0] = 1
            for i in range(1, n+1):
                for j in range(1, s+1):
                    if coin[i-1] <= j:
                        dp[i][j] = dp[i-1][j] + dp[i][j-coin[i-1]]
                    else:
                        dp[i][j] = dp[i-1][j]
            return dp[n][s]

        if __name__ == '__main__':
            coin = [1, 2, 3]
            _sum = 4
            print(ccp(coin, _sum))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        int ccp(vector<int> coin, int _sum) {
            int n = coin.size();
            int s = _sum;
            int dp[n+1][s+1] = {};
            for (int i=1; i<=n; ++i) {
                dp[i][0] = 1;
            }
            for (int i=1; i<=n; ++i) {
                for (int j=1; j<=s; ++j) {
                    if (coin[i-1] <= j) {
                        dp[i][j] = dp[i-1][j] + dp[i][j-coin[i-1]];
                    } else {
                        dp[i][j] = dp[i-1][j];
                    }
                }
            }
            return dp[n][s];
        }

        int main() {
            vector<int> coin{1, 2, 3};
            int _sum = 4;
            cout << ccp(coin, _sum);
        }

    .. code-tab:: java

        class CCP {
            static int ccp(int coin[], int _sum) {
                int n = coin.length;
                int s = _sum;
                int dp[][] = new int[n+1][s+1];
                for (int i=1; i<=n; ++i) {
                    dp[i][0] = 1;
                }
                for (int i=1; i<=n; ++i) {
                    for (int j=1; j<=s; ++j) {
                        if (coin[i-1] <= j) {
                            dp[i][j] = dp[i-1][j] + dp[i][j-coin[i-1]];
                        } else {
                            dp[i][j] = dp[i-1][j];
                        }
                    }
                }
                return dp[n][s];
            }
            public static void main(String args[]) {
                int coin[] = {1, 2, 3};
                int _sum = 4;
                System.out.println(ccp(coin, _sum));
            }
        }

Word Break Problem
------------------

:Time Complexity: :math:`O(N^2)`
:Auxiliary Space: :math:`O(N^2)`

.. tabs::

    .. code-tab:: python

        def wordin(w, _dict):
            for d in _dict:
                if w == d:
                    return True
            return False

        def wbp(s, _dict):
            n = len(s)
            dp = [False for i in range(n+1)]
            dp[0] = True
            for i in range(1, n+1):
                for j in range(i):
                    if dp[j] == True and wordin(s[j:i], _dict):
                        dp[i] = True
                        break
            return dp[n]

        if __name__ == '__main__':
            _dict = ["mobile","samsung","sam","sung","man","mango","icecream","and","go","i","like","ice","cream"]
            print(wbp("ilikesamsung", _dict))
            print(wbp("iiiiiiii", _dict))
            print(wbp("", _dict))
            print(wbp("ilikelikeimangoiii", _dict))
            print(wbp("samsungandmango", _dict))
            print(wbp("samsungandmangok", _dict))

    .. code-tab:: cpp

        # include <bits/stdc++.h>
        using namespace std;

        bool wordin(string w, vector<string> _dict) {
            for (string d : _dict) {
                if (w == d) {
                    return true;
                }
            }
            return false;
        }

        bool wbp(string s, vector<string> _dict) {
            int n = s.length();
            bool dp[n+1] = {};
            dp[0] = true;
            for (int i=1; i<=n; ++i) {
                for (int j=0; j<i; ++j) {
                    if (dp[j] && wordin(s.substr(j, i-j), _dict)) {
                        dp[i] = true;
                        break;
                    }
                }
            }
            return dp[n];
        }

        int main() {
            vector<string> _dict{"mobile","samsung","sam","sung","man","mango","icecream","and","go","i","like","ice","cream"};
            cout << wbp("ilikesamsung", _dict) << endl;
            cout << wbp("iiiiiiii", _dict) << endl;
            cout << wbp("", _dict) << endl;
            cout << wbp("ilikelikeimangoiii", _dict) << endl;
            cout << wbp("samsungandmango", _dict) << endl;
            cout << wbp("samsungandmangok", _dict) << endl;
        }

    .. code-tab:: java

        class WBP {
            static boolean wordin(String w, String _dict[]) {
                for (String d : _dict) {
                    if (w.equals(d)) {
                        return true;
                    }
                }
                return false;
            }
            static boolean wbp(String s, String _dict[]) {
                int n = s.length();
                boolean dp[] = new boolean[n+1];
                dp[0] = true;
                for (int i=1; i<=n; ++i) {
                    for (int j=0; j<i; ++j) {
                        if (dp[j] && wordin(s.substring(j, i), _dict)) {
                            dp[i] = true;
                            break;  
                        }
                    }
                }
                return dp[n];
            }
            public static void main(String args[]) {
                String _dict[] = {"mobile","samsung","sam","sung","man","mango","icecream","and","go","i","like","ice","cream"};
                System.out.println(wbp("ilikesamsung", _dict));
                System.out.println(wbp("iiiiiiii", _dict));
                System.out.println(wbp("", _dict));
                System.out.println(wbp("ilikelikeimangoiii", _dict));
                System.out.println(wbp("samsungandmango", _dict));
                System.out.println(wbp("samsungandmangok", _dict));
            }
        }