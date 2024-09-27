clc; clear all; close all;

dt = 0.1;
T = 108; %(2012-2021 = 108 bulan)
n = T/dt; %jumlah iterasi

t = 0:dt:T;

for i = 1:101
    contact_rate_arr(i) = (i-1)*0.001;
end

for j = 1:length(contact_rate_arr)
    recruitment = 0.0042;
    contact_rate = contact_rate_arr(j);
    death_rate = 0.01;
    conversion_rate = 0.03;
    incubation_period = 0.17;
    negotiation_rate = 0.12;
    reconciled_rate_2 = 0.13;
    reconciled_rate_e = 0.11;
    S(1) = 100;
    E(1) = 6;
    P(1) = 4;
    H(1) = 1;
    R(1) = 0;
    
    s = @(S,E,P,H,R) recruitment-contact_rate*S*P-death_rate*S;
    e = @(S,E,P,H,R) contact_rate*S*P-(death_rate+conversion_rate+incubation_period)*E;
    p = @(S,E,P,H,R) incubation_period*E-(death_rate+negotiation_rate+reconciled_rate_2)*P;
    h = @(S,E,P,H,R) negotiation_rate*P-(death_rate+reconciled_rate_e)*H;
    r = @(S,E,P,H,R) reconciled_rate_e*H+reconciled_rate_2*P+conversion_rate*E-death_rate*R;
    
    for i = 1:n
        s1 = s(S(i),E(i),P(i),H(i),R(i));
        e1 = e(S(i),E(i),P(i),H(i),R(i));
        p1 = p(S(i),E(i),P(i),H(i),R(i));
        h1 = h(S(i),E(i),P(i),H(i),R(i));
        r1 = r(S(i),E(i),P(i),H(i),R(i));
        
        s2 = s(S(i)+(dt/2)*s1,E(i)+(dt/2)*e1,P(i)+(dt/2)*p1,H(i)+(dt/2)*h1,R(i)+(dt/2)*r1);
        e2 = e(S(i)+(dt/2)*s1,E(i)+(dt/2)*e1,P(i)+(dt/2)*p1,H(i)+(dt/2)*h1,R(i)+(dt/2)*r1);
        p2 = p(S(i)+(dt/2)*s1,E(i)+(dt/2)*e1,P(i)+(dt/2)*p1,H(i)+(dt/2)*h1,R(i)+(dt/2)*r1);
        h2 = h(S(i)+(dt/2)*s1,E(i)+(dt/2)*e1,P(i)+(dt/2)*p1,H(i)+(dt/2)*h1,R(i)+(dt/2)*r1);
        r2 = r(S(i)+(dt/2)*s1,E(i)+(dt/2)*e1,P(i)+(dt/2)*p1,H(i)+(dt/2)*h1,R(i)+(dt/2)*r1);
        
        s3 = s(S(i)+(dt/2)*s2,E(i)+(dt/2)*e2,P(i)+(dt/2)*p2,H(i)+(dt/2)*h2,R(i)+(dt/2)*r2);
        e3 = e(S(i)+(dt/2)*s2,E(i)+(dt/2)*e2,P(i)+(dt/2)*p2,H(i)+(dt/2)*h2,R(i)+(dt/2)*r2);
        p3 = p(S(i)+(dt/2)*s2,E(i)+(dt/2)*e2,P(i)+(dt/2)*p2,H(i)+(dt/2)*h2,R(i)+(dt/2)*r2);
        h3 = h(S(i)+(dt/2)*s2,E(i)+(dt/2)*e2,P(i)+(dt/2)*p2,H(i)+(dt/2)*h2,R(i)+(dt/2)*r2);
        r3 = r(S(i)+(dt/2)*s2,E(i)+(dt/2)*e2,P(i)+(dt/2)*p2,H(i)+(dt/2)*h2,R(i)+(dt/2)*r2);
       
        s4 = s(S(i)+s3*dt,E(i)+e3*dt,P(i)+p3*dt,H(i)+h3*dt,R(i)+r3*dt);
        e4 = e(S(i)+s3*dt,E(i)+e3*dt,P(i)+p3*dt,H(i)+h3*dt,R(i)+r3*dt);
        p4 = p(S(i)+s3*dt,E(i)+e3*dt,P(i)+p3*dt,H(i)+h3*dt,R(i)+r3*dt);
        h4 = h(S(i)+s3*dt,E(i)+e3*dt,P(i)+p3*dt,H(i)+h3*dt,R(i)+r3*dt);
        r4 = r(S(i)+s3*dt,E(i)+e3*dt,P(i)+p3*dt,H(i)+h3*dt,R(i)+r3*dt);
        
        S(i+1) = S(i)+(dt/6)*(s1+(2*s2)+(2*s3)+s4);
        E(i+1) = E(i)+(dt/6)*(e1+(2*e2)+(2*e3)+e4);
        P(i+1) = P(i)+(dt/6)*(p1+(2*p2)+(2*p3)+p4);
        H(i+1) = H(i)+(dt/6)*(h1+(2*h2)+(2*h3)+h4);
        R(i+1) = R(i)+(dt/6)*(r1+(2*r2)+(2*r3)+r4);
    end
    plot(t, S, 'DisplayName', "S(t)")
    legend('show','Interpreter','latex','Location',"best")
    hold on
    plot(t, E, 'DisplayName', "E(t)")
    plot(t, P, 'DisplayName', "P(t)")
    plot(t, H, 'DisplayName', "H(t)")
    plot(t, R, 'DisplayName', "R(t)")
    hold off
    title("Animasi Pengaruh Contact Rate \beta = "+contact_rate_arr(j)+" pada Model SEPHR")
    drawnow
    pause(0.2)
end
