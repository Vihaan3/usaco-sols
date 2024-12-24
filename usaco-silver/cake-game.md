# Cake Game

````cpp
#include <bits/stdc++.h>
using namespace std;

void solve()
{
	int n;
	cin >> n;
	vector<long long> prefix (n+1);
	vector <long long> arr (n);

	for (int i = 0; i < n; i++)
	{
		cin >> arr[i];
	}

	prefix[1] = arr[0];
	for (int i = 1; i < n; i++)
	{
		prefix[i+1] = prefix[i] + arr[i];
	}

	int window = n/2 + 1;
	long long ans = LLONG_MAX;
	for (int i = 0; i + window < n+1; i++)
	{
		ans = min(ans, prefix[i+window]-prefix[i]);
	}

	cout << ans << " " << prefix[n]-ans << endl;
}

int main() {
	int T;
	cin >> T;
	while (T--)
	{solve();}
}
```
````

