Dynamic Programming 
===================

Longest Common Subsequence 
--------------------------

:Time Complexity: :math:`O(M\times N)`
:Auxiliary Space: :math:`O(M\times N)`

.. tabs::

    .. code-tab:: python

        def lcs(X, Y):
            dp = [[0 for j in range(len(Y)+1)] for i in range(len(X)+1)]
            for i in range(1, len(X)+1):
                for j in range(1, len(Y)+1):
                    if X[i-1] == Y[j-1]:
                        dp[i][j] = dp[i-1][j-1] + 1
                    else:
                        dp[i][j] = max(dp[i-1][j], dp[i][j-1])
            return dp[len(X)][len(Y)]

        if __name__ == '__main__':
            X = "AGGTAB"
            Y = "GXTXAYB"
            print(lcs(X, Y))

    .. code-tab:: cpp

        #include <bits/stdc++.h>
        using namespace std;

        int lcs(string X, string Y) {
            int dp[X.length()+1][Y.length()+1] = {};
            for (int i=1; i<=X.length(); ++i) {
                for (int j=1; j<=Y.length(); ++j) {
                    if (X[i-1] == Y[j-1]) {
                        dp[i][j] = dp[i-1][j-1] + 1;
                    } else {
                        dp[i][j] = (dp[i-1][j] > dp[i][j-1]) ? dp[i-1][j] : dp[i][j-1];
                    }
                }
            }
            return dp[X.length()][Y.length()];
        }

        int main() {
            string X = "AGGTAB";
            string Y = "GXTXAYB";
            cout << lcs(X, Y);
        }

    .. code-tab:: java

        class LCS {
            static int lcs(String X, String Y) {
                int dp[][] = new int[X.length()+1][Y.length()+1];
                for (int i=1; i<=X.length(); ++i) {
                    for (int j=1; j<=Y.length(); ++j) {
                        if (X.charAt(i-1) == Y.charAt(j-1)) {
                            dp[i][j] = dp[i-1][j-1] + 1;
                        } else {
                            dp[i][j] = (dp[i-1][j] > dp[i][j-1]) ? dp[i-1][j] : dp[i][j-1];
                        }
                    }
                }
                return dp[X.length()][Y.length()];
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
            dp = [1 for i in range(len(arr))]
            for i in range(1, len(arr)):
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

        int lis(int arr[], int n) {
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
            int arr[] = {10, 22, 9, 33, 21, 50, 41, 60};
            cout << lis(arr, 8);
        }

    .. code-tab:: java

        class LIS {
            static int lis(int arr[]) {
                int dp[] = new int[arr.length];
                for (int i=0; i<dp.length; ++i) {
                    dp[i] = 1;
                }
                for (int i=1; i<dp.length; ++i) {
                    for (int j=0; j<i; ++j) {
                        if (arr[j]<arr[i] && dp[j]+1>dp[i]) {
                            dp[i] = dp[j] + 1;
                        }
                    }
                }
                int maxL = 1;
                for (int i=0; i<dp.length; ++i) {
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

:Time Complexity: :math:`O(M\times N)`
:Auxiliary Space: :math:`O(M\times N)`

.. tabs::

    .. code-tab:: python

        def ed(X, Y):
            dp = [[0 for j in range(len(Y)+1)] for i in range(len(X)+1)]
            for i in range(len(X)+1):
                dp[i][0] = i
            for j in range(len(Y)+1):
                dp[0][j] = j
            for i in range(1, len(X)+1):
                for j in range(1, len(Y)+1):
                    if X[i-1] == Y[j-1]:
                        dp[i][j] = dp[i-1][j-1]
                    else:
                        dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1
            return dp[len(X)][len(Y)]

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
            int dp[X.length()+1][Y.length()+1];
            for (int i=0; i<=X.length(); ++i) {
                dp[i][0] = i;
            }
            for (int j=0; j<=Y.length(); ++j) {
                dp[0][j] = j;
            }
            for (int i=1; i<=X.length(); ++i) {
                for (int j=1; j<=Y.length(); ++j) {
                    if (X[i-1]==Y[j-1]) {
                        dp[i][j] = dp[i-1][j-1];
                    } else {
                        dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1;
                    }
                }
            }
            return dp[X.length()][Y.length()];
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
                int dp[][] = new int[X.length()+1][Y.length()+1];
                for (int i=0; i<=X.length(); ++i) {
                    dp[i][0] = i;
                }
                for (int j=0; j<Y.length(); ++j) {
                    dp[0][j] = j;
                }
                for (int i=1; i<=X.length(); ++i) {
                    for (int j=1; j<=Y.length(); ++j) {
                        if (X.charAt(i-1)==Y.charAt(j-1)) {
                            dp[i][j] = dp[i-1][j-1];
                        } else {
                            dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1;
                        }
                    }
                }
                return dp[X.length()][Y.length()];
            }
            public static void main(String args[]) {
                String X = "sunday";
                String Y = "saturday";
                System.out.println(ed(X, Y));
            }
        }