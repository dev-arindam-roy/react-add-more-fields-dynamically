# Add more dynamic fields - React Js

### Check It - 

[https://dev-arindam-roy.github.io/react-add-more-fields-dynamically](https://dev-arindam-roy.github.io/react-add-more-fields-dynamically)

```js
import React, { useState } from "react";

const App = () => {
  const [skills, setSkills] = useState([""]);
  const [mySkills, setMySkills] = useState([]);

  const skillNameHandler = (event, index) => {
    let skillList = [...skills];
    skillList[index] = event.target.value;
    setSkills(skillList);
  };

  const addSkillHandler = () => {
    setSkills([...skills, []]);
  };

  const deleteSkillHandler = (index) => {
    let skillList = [...skills];
    skillList.splice(index, 1);
    setSkills(skillList);
  };

  const formSubmitHandler = (e) => {
    e.preventDefault();
    setMySkills(skills);
    setSkills(['']);
  };

  return (
    <>
      <div className="container">
        <div className="row mt-5">
          <div className="col-md-3">
            <form onSubmit={formSubmitHandler}>
              <div className="form-group">
                <label>Skill (s):</label>
              </div>
              {skills.length > 0 &&
                skills.map((item, index) => {
                  return (
                    <div className="form-group mt-2" key={index}>
                      <input
                        type="text"
                        id={"skillName" + index}
                        className="form-control"
                        placeholder="Skill Name"
                        required
                        value={item}
                        onChange={(e) => skillNameHandler(e, index)}
                      />

                      <button
                        type="button"
                        id={"deleteBtn" + index}
                        className={
                          "btn btn-sm btn-danger mt-1" +
                          (index === 0 ? " d-none" : "")
                        }
                        onClick={() => deleteSkillHandler(index)}
                      >
                        [-]
                      </button>
                    </div>
                  );
                })}

              <div className="form-group mt-2" style={{ textAlign: "right" }}>
                <button
                  type="button"
                  className="btn btn-sm btn-primary"
                  onClick={addSkillHandler}
                >
                  [+]
                </button>
              </div>
              <div
                className={
                  "form-group mt-3 " + (skills.length < 2 ? "d-none" : "")
                }
              >
                <button type="submit" className="btn btn-sm btn-success">
                  Save
                </button>
              </div>
            </form>
          </div>
          <div className="col-md-6">
            {
              mySkills.length > 0 && (
                <h4>Skills ({mySkills.length})</h4>
              )
            }
            {
              mySkills.length > 0 && (
                mySkills.map((skill, index) => {
                  return (
                    <li key={index}>{skill.toUpperCase()}</li>
                  )
                })
              )
            }
            {
              mySkills.length === 0 && (
                <label>......</label>
              )
            }
          </div>
        </div>
      </div>
    </>
  );
};

export default App;

```