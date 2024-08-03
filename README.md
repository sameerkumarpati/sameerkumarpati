import streamlit as st
import numpy as np

# Create a Streamlit app
st.title("NRR Calculator")

# Divide the website into two sections
left_column, right_column = st.columns(2)

# Left section: Sliders for runs, overs, wickets
with left_column:
    st.header("Input")
    csk_runs = st.slider("CSK Runs", 1, 300, 150)
    csk_overs = st.slider("CSK Overs", 1, 20, 10)
    csk_wickets = st.slider("CSK Wickets", 1, 10, 5)
    rcb_runs = st.slider("RCB Runs", 1, 300, 150)
    rcb_overs = st.slider("RCB Overs", 1, 20, 10)
    rcb_wickets = st.slider("RCB Wickets", 1, 10, 5)

# Right section: Display runs, overs, wickets, and NRR
with right_column:
    st.header("Output")
    st.write("CSK:")
    st.write(f"Runs: {csk_runs}")
    st.write(f"Overs: {csk_overs}")
    st.write(f"Wickets: {csk_wickets}")
    st.write("RCB:")
    st.write(f"Runs: {rcb_runs}")
    st.write(f"Overs: {rcb_overs}")
    st.write(f"Wickets: {rcb_wickets}")

    # Calculate NRR
    if csk_runs > rcb_runs:
        winner = "CSK"
        nrr_csk = (csk_runs / csk_overs) - (rcb_runs / rcb_overs)
        nrr_rcb = None
    elif rcb_runs > csk_runs:
        winner = "RCB"
        nrr_rcb = (rcb_runs / rcb_overs) - (csk_runs / csk_overs)
        nrr_csk = None
    else:
        winner = "Draw"
        nrr_csk = None
        nrr_rcb = None

    st.write(f"Winner: {winner}")
    if nrr_csk is not None:
        st.write(f"CSK NRR: {nrr_csk:.2f}")
    if nrr_rcb is not None:
        st.write(f"RCB NRR: {nrr_rcb:.2f}")
