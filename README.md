import React, { Component } from "react";

class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      Person: {
        fullName: "John Doe",
        bio: "A passionate developer with experience in React and Node.js.",
        imgSrc: "https://via.placeholder.com/150",
        profession: "Software Developer",
      },
      shows: false,
      mountedTime: 0,
    };
  }

  componentDidMount() {
    this.interval = setInterval(() => {
      this.setState((prevState) => ({ mountedTime: prevState.mountedTime + 1 }));
    }, 1000);
  }

  componentWillUnmount() {
    clearInterval(this.interval);
  }

  toggleProfile = () => {
    this.setState((prevState) => ({ shows: !prevState.shows }));
  };

  render() {
    const { Person, shows, mountedTime } = this.state;
    return (
      <div style={{ textAlign: "center", marginTop: "20px" }}>
        <button onClick={this.toggleProfile} style={{ padding: "10px 20px", fontSize: "16px" }}>
          {shows ? "Hide Profile" : "Show Profile"}
        </button>
        {shows && (
          <div style={{ marginTop: "20px" }}>
            <img src={Person.imgSrc} alt="profile" style={{ borderRadius: "50%", width: "150px", height: "150px" }} />
            <h2>{Person.fullName}</h2>
            <p>{Person.bio}</p>
            <h3>{Person.profession}</h3>
          </div>
        )}
        <div style={{ marginTop: "20px" }}>
          <p>Time since component mounted: {mountedTime} seconds</p>
        </div>
      </div>
    );
  }
}

export default App;
