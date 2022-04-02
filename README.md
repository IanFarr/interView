# interView
### [Live site](https://interview-mern.herokuapp.com/#/)

## Overview

interView is a video interviewing platform where users can practice their interviewing skills and elicit feedback to continually improve
themselves. interView seeks to make the interviewing process more successful by connecting users with people who are also interviewing and by
providing a medium to continually work on improving users' interview performance. 

With interView, users can create accounts and upload videos of themselves answering popular interview questions. Once the video is on interView,
other users can view it and provide constructive feedback. Feedback is provided in twor forms: text and a rubric. Text feedback is broken into two
categories - positive and negative. Users are told both what they did well and how they can improve. The rubric scores a user's specific
interviewing skills so they can focus on what is required to see the most improvement.

## Features Highlights
- Upload video-form answers to variant behavioral questions. 
- Display videos on the home page regarding different behavioral questions.
- Receive feedback for uploaded videos and give feedback on other users’ videos. 
- Edit/delete authorized feedback.
- View/elicit specific scoring rubric on videos. 

## Technologies
<code><img height="30" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-original.svg" alt="javascript"></code>
<code><img height="30" src="https://github.com/devicons/devicon/blob/master/icons/html5/html5-original.svg" alt="html5"></code>
<code><img height="30" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original.svg" alt="css3"></code>
<code><img height="30" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/react/react-original.svg" alt="react.js"></code>
<code><img height="30" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/express/express-original.svg" alt="express.js"></code>
<code><img height="30" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/nodejs/nodejs-original.svg" alt="node.js"></code>
<code><img height="30" src="https://github.com/devicons/devicon/blob/master/icons/mongodb/mongodb-original.svg" alt="mongodb"></code>
<code><img height="30" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/amazonwebservices/amazonwebservices-original.svg" alt="aws s3"></code>
<code><img height="30" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/heroku/heroku-original.svg" alt="heroku"></code>

### MERN Stack
- Our data storage and recall is handled through ***MongoDB***:

```
const VideoSchema = new Schema({
    user: {
        type: Schema.Types.ObjectId,
        ref: 'users'
    },
    file: {
        type: Object,
        required: true
    },
    views: {
        type: Number,
        default: 0
    },
    question: {
        type: String,
        required: true
    },
    experience: {
        type: String,
        required: true
    },
    industry: {
        type: String,
        required: true
    }
}, {
    timestamps: true
});
```

- interView uses a light weight ***Express.js*** back end application framework

```
router.get('/feedbacks/:id', (req, res) => {
    Feedback.find({ video: req.params.id })
        .then(feedback => res.json(feedback))
        .catch(err =>
            res.status(404).json({ nofeedbackfound: 'No video found with that ID' })
        );
});
```

- correct and dynamic information is presented to the user using a ***React/Redux*** frontend

```
render() {
  const { videos } = this.props;

  return (
    <div className='show-video-background'>
      <div className='mainbox'>
        <div className='playing-video-container'>
          <ShowVideoDisplay video={this.props.video} fetchVideo={this.props.fetchVideo} videoId={this.props.videoId}/>
          <ShowFeedbacksContainer videoId={this.props.videoId} history={this.props.history}/>
        </div>
        <div className='sidebar'>
          <h2>Average Scores</h2>
          <ShowRubricsContainer videoId={this.props.videoId} />
          <RubricFormContainer videoId={this.props.videoId} />
          <br className='checkout-other'/>
          <div className='other-videos-container'>
            <div className='other-thumbnails-container'>
              {
                videos.map((video, idx) => (
                  <VideoItem key={idx} video={video} image={pics[idx]} />
                ))
              }
            </div>
          </div>
        </div>
      </div>
    </div>
  );
}
```

- ***Node.js*** is the runtime environment that makes it all work together

```
let proWidth = (this.props.avgrubrics.professionalismRating / 5) * 100 + '%';
        let confWidth = (this.props.avgrubrics.confidenceRating / 5) * 100 + '%';
        let contWidth = (this.props.avgrubrics.contentRating / 5) * 100 + '%';
        let voiWidth = (this.props.avgrubrics.voiceRating / 5) * 100 + '%';
        let average = (
            ((this.props.avgrubrics.professionalismRating)
                + (this.props.avgrubrics.confidenceRating)
                + (this.props.avgrubrics.contentRating)
                + (this.props.avgrubrics.voiceRating)) / 4
        ).toFixed(1); 
```


## Design Previews

#### Mainpage  
<img src="https://github.com/hwkcode/interView/blob/main/frontend/public/interViewlink.png"/>

#### Signup
<img src="https://github.com/hwkcode/interView/blob/main/frontend/public/Signup.png"/>

#### Homepage
<img src="https://github.com/hwkcode/interView/blob/main/frontend/public/Home.png"/>

#### Viewpage
<img src="https://github.com/hwkcode/interView/blob/main/frontend/public/View.png"/>

#### Feedback
<img src="https://github.com/hwkcode/interView/blob/main/frontend/public/Feedback.png"/>
