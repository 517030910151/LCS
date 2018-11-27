# LCS
最长公共子序列在数据较多时的做法
    
    #include<algorithm>
    #include<iostream>
    #include<cstdio>
    using namespace std;
    const int MAXN = 100005;
    int n, m, map1[MAXN], dp[MAXN], a[MAXN];
 
    int longestIncreaseSubArr() {
	    dp[0] = 1;
	    for (int i = 1; i < n; i++) {
		    int max = 1;
		    for (int j = 0; j < i; j++) {
		    	if (a[i] > a[j] && dp[j] >= max) {
			    	max = dp[j] + 1;
		    	}
		    }
		    dp[i] = max;
	    }
 
	    return dp[n - 1];
    }
 
    int main()
    {
	ios::sync_with_stdio(0);
	cin.tie(0); cout.tie(0);
	int i;
	cin >> n;
	for (i = 1; i <= n; i++)
	{
		int x;
		cin >> x;
		map1[x] = i;
	}
	for (i = 1; i <= n; i++)
	{
		int x;
		cin >> x;
		a[i] = map1[x];//a[i]存x在第一个序列中的位置
	}
	//cout << longestIncreaseSubArr() << '\n';
	for (i = 1; i <= n; i++)
	{
	    if (a[i]>dp[m])
	        dp[++m] = a[i];
	    else {
	        dp[lower_bound(dp + 1, dp + m + 1, a[i]) - dp] = a[i];//为了使dp[]始终存最小的数,找a[i]最长上升序列长度就是答案
	    }
	}
	cout << m << '\n';
	return 0;
  }
