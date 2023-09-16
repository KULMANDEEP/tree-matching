# tree-matching


#include<bits/stdc++.h>
using namespace std;
void solve(int src, int par, vector<int>adj[], vector<vector<long long>>&dp){
    dp[src][0]=0, dp[src][1]=0;
    int leaf=1;
    
    for(auto child:adj[src]){
        if(child!=par){
            leaf=0;
            solve(child, src, adj, dp);
        }
    }
    if(leaf)return;
    
    for(auto child : adj[src]){
        if(child!=par){
            dp[src][0] += max(dp[child][0], dp[child][1]);
        }
        
    }
    for(auto child : adj[src]){
        if(child!=par){
            dp[src][1] = max(dp[src][1], 1 + dp[child][0] + (dp[src][0]- max(dp[child][0], dp[child][1])));
        }
    }
}

int main(){
    int nodes;
    cin>>nodes;
    vector<int>adj[nodes+1];
    vector<vector<long long>>dp(nodes+1, vector<long long>(2, -1));
    for(int i=1;i<nodes;i++){
        int x, y;
        cin>>x>>y;
        adj[x].push_back(y);
        adj[y].push_back(x);
        
    }
    solve(1, 0, adj, dp);
    cout<<max(dp[1][0], dp[1][1]);
    return 0;
}
