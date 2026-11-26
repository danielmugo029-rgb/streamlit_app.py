
import streamlit as st
from datetime import datetime
from PIL import Image

st.set_page_config(
    page_title="Smart Fire Detection System",
    page_icon="🔥",
    layout="wide"
)

if "alerts" not in st.session_state:
    st.session_state.alerts = []

st.title("🔥 Smart Fire Detection and Alarm System")
st.caption("Intelligent Fire Monitoring Dashboard")

st.sidebar.title("Navigation")

page = st.sidebar.radio(
    "Select Section",
    [
        "Dashboard",
        "Fire Detection",
        "Alert History",
        "About Project"
    ]
)

if page == "Dashboard":

    st.header("System Dashboard")

    col1, col2, col3 = st.columns(3)

    col1.metric("System Status", "ONLINE")
    col2.metric("Fire Alerts", len(st.session_state.alerts))
    col3.metric("AI Engine", "NOT CONNECTED")

    st.info(
        "Dashboard is operational. "
        "Connect your trained AI model to enable actual detection."
    )

    st.subheader("System Features")

    st.write("🔥 Fire detection")
    st.write("💨 Smoke detection")
    st.write("📷 Image analysis")
    st.write("🚨 Alert monitoring")
    st.write("📊 Detection history")

elif page == "Fire Detection":

    st.header("Fire and Smoke Detection")

    uploaded_file = st.file_uploader(
        "Upload an image for analysis",
        type=["jpg", "jpeg", "png"]
    )

    if uploaded_file:

        image = Image.open(uploaded_file)

        st.image(
            image,
            caption="Uploaded Image",
            use_container_width=True
        )

        if st.button("Analyse Image"):

            st.warning(
                "AI detection engine is not connected yet. "
                "No fire detection result has been generated."
            )

elif page == "Alert History":

    st.header("Detection Alert History")

    if st.session_state.alerts:

        for alert in st.session_state.alerts:
            st.write(alert)

    else:
        st.info("No alerts recorded yet.")

elif page == "About Project":

    st.header("About the Project")

    st.write("""
    Smart Fire Detection and Alarm System.

    Developed by: Daniel Ng'enyi Mugo

    Supervisor: Wilfred Odoyo

    The project explores intelligent fire and smoke
    detection using Python and artificial intelligence.
    """)

    st.warning(
        "This is an academic demonstration prototype, "
        "not a certified fire safety system."
    )
