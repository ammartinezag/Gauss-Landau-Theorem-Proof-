:: Aguilera, M. M. "A Formal Proof of the Gauss-Landau Theorem"
:: Submitted to the Mizar Mathematical Library, 2024.

environ

 vocabularies NUMBERS, NAT_1, SUBSET_1, ORDINAL1, ARYTM_3, XXREAL_0, CARD_3,
      ARYTM_1, RELAT_1, TARSKI, FINSEQ_1, FUNCT_1, XBOOLE_0, FINSET_1, NEWTON,
      NAT_3, INT_2, NAT_6;

 notations TARSKI, XBOOLE_0, SUBSET_1, ORDINAL1, NUMBERS, XCMPLX_0, XXREAL_0,
      FINSET_1, FUNCT_1, FINSEQ_1, NEWTON, INT_2, NAT_3, NAT_6;

 constructors XXREAL_0, NAT_D, NEWTON, NAT_3, PEPIN, NAT_6;

 registrations XXREAL_0, MEMBERED, NEWTON, NAT_3, NAT_6;

 theorems NEWTON, NAT_3, NAT_6, XTUPLE_0;

begin :: Main Formalization

 reserve S for non empty finite Subset of NAT;
 reserve p for Prime;
 reserve n, k, d for Nat;

definition
  let S be non empty finite Subset of NAT;
  func min_exp(S) -> ManySortedSet of SetPrimes means
  :Def1:
    for p being Prime holds it.p = min { p |-count n where n is Element of S : n in S };
  existence ... end; :: Proof of existence here
  uniqueness ... end; :: Proof of uniqueness here
end;

:: Lemma 1: d divides n iff for all primes p, v_p(d) <= v_p(n)
theorem Th1:
  for d, n being Nat st d > 0 & n > 0 holds
    (d divides n iff for p being Prime holds p |-count d <= p |-count n)
proof
  ... :: Formal proof using NAT_3:57, THEORY_OF_FTA, etc.
end;

:: Lemma 2: The product of p^{min_p} divides all n in S and is the greatest such number
theorem Th2:
  for S being non empty finite Subset of NAT,
      d being Nat
  st d = Product (p |-> (min_exp(S)).p)
  holds
    (for n being Element of S holds d divides n) &
    (for d' being Nat st (for n being Element of S holds d' divides n) holds d' divides d)
proof
  ... :: Formal proof using Th1, properties of min, and the product
end;

:: Main Theorem: Part 1 - GCD
theorem
  for S being non empty finite Subset of NAT
  holds gcd S = Product (p |-> (min_exp(S)).p)
proof
  let S be non empty finite Subset of NAT;
  set d = Product (p |-> (min_exp(S)).p);
  A1: for n being Element of S holds d divides n by Th2;
  A2: for d' being Nat st (for n being Element of S holds d' divides n) holds d' divides d by Th2;
  thus thesis by A1, A2, NAT_6:def 3; :: Using the official Mizar definition of gcd
end;

:: Main Theorem: Part 2 - LCM (similar structure)
theorem
  ...
end;

end.
