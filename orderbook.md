---
layout: landing
title: Freiexchange order book re-charted
description: Plots of order books obtained via Freiexchange’s API, edited for sanity.
category: graphs
tags: gapcoin
---
  <div class="ui vertical segment">
    <div class="ui very relaxed stackable page grid">
      <div class="row">
        <div class="column">
          <div class="ui raised padded container segment">
            <div class="ui animated selection list">
            {% for retrieval in site.orderbook %}
              <a class="item" href="{{ retrieval.url }}">
                <div class="ui header" style="padding: 0.6em">
                  <i class="blue chart line icon"></i>
                    {{ retrieval.title }} for {{ retrieval.date | date_to_string}}
                </div>
              </a>
            {% endfor %}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
