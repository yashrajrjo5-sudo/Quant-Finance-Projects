# Binomial tree European option pricing model
# Initialise Parameters
S0=100
K=100
T=1
N=3
u=1.1
d=1/u
opttype='C'
import numpy as np
def binomial_tree(K,T,S0,N,u,d,opttype):
# precompute Constants
dt=T/N
q=(np.exp(r*dt)-d)/(u-d)
disc=np.exp(-r*dt)
# Initialise assest prices at maturity- Time step N
S=np.zeros(N+1)
S[0]=S0*d**N
for j in range (1,N+1):
S[j]=S[j-1]*u/d
# Initialise option values at maturity
C=np.zeros(N+1)
for j in range(0,N+1):
C[j]=max(0,S[j]-K)
# Step backwards through tree
for i in np.arange (N,0,-1):
    for j in range (0,i):
        C[j]=disc*(q*C(j+1)+(1-q)*C[j])
return C[0]        
        
