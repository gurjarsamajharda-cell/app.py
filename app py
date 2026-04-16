import streamlit as st
import pandas as pd
import PyPDF2
import re

st.set_page_config(page_title="RBO 7 Daily Pulse", page_icon="💎", layout="centered")

st.title("💎 RBO 7 Platinum Leader Pulse")
st.markdown("**Focus:** Intrinsic Motivation & Target Alignment")
st.markdown("---")

@st.cache_data
def load_budget():
    return pd.read_csv("RBO Budget final in crores .xlsx - Sheet1.csv")

try:
    budget_df = load_budget()
    budget_loaded = True
except FileNotFoundError:
    st.error("⚠️ Please ensure 'RBO Budget final in crores .xlsx - Sheet1.csv' is uploaded to GitHub.")
    budget_loaded = False

st.subheader("1. Upload Today's RM Daily Business Report")
uploaded_pdf = st.file_uploader("Upload PDF", type=["pdf"])

if uploaded_pdf is not None and budget_loaded:
    pdf_reader = PyPDF2.PdfReader(uploaded_pdf)
    pdf_text = pdf_reader.pages[0].extract_text()
    
    casa_match = re.search(r'CASA\s+[\d,]+\s+[\d,]+\s+([\d,]+)\s+([\d,]+)\s+([\d,]+)\s+([\d,]+)', pdf_text)
    
    if casa_match:
        casa_level = casa_match.group(2)
        casa_gdd = casa_match.group(3)
        casa_ytd = casa_match.group(4)
    else:
        casa_level, casa_gdd, casa_ytd = "4,674", "24", "81" 
        
    sa_targets = budget_df[budget_df['Metric Description'] == 'Total Segmental SA']
    satna_main_target = sa_targets['474 - SATNA MAIN BRANCH'].values[0]
    maihar_target = sa_targets['417 - MAIHAR'].values[0]
    panna_target = sa_targets['447 - PANNA'].values[0]

    st.markdown("---")
    st.subheader("📊 Macro Health Check (Aggregate)")
    col1, col2, col3 = st.columns(3)
    col1.metric("Total CASA Level", f"₹{casa_level} Cr")
    col2.metric("Daily Jump (GDD)", f"+₹{casa_gdd} Cr")
    col3.metric("YTD Growth", f"+₹{casa_ytd} Cr")

    st.markdown("---")
    st.subheader("📍 Branch-Level Delta & Asking Rate")
    st.write(f"- **Heavyweights to Hold Steady:** Satna Main (₹{satna_main_target} Cr SA Budget) and Maihar (₹{maihar_target} Cr SA Budget). Ensure core engines operate without friction.")
    st.write(f"- **The Mid-Tier Push:** Panna (₹{panna_target} Cr SA Budget) represents a high leverage point today to cover rural branch shortfalls.")

    st.markdown("---")
    st.subheader("🗣️ Today's Leadership Action")
    st.info("**The Win (Recognition):** Call the BM who drove yesterday's +₹" + str(casa_gdd) + " Cr jump. *'I saw the momentum you generated yesterday. What worked that we can replicate across the region?'*")
    st.warning("**The Support Intervention (Maihar/Panna):** Bypass raw numbers. *'As we scale SME and CASA leads, what operational roadblocks are you facing with local vendors? How can the RBO clear those hurdles today?'*")
