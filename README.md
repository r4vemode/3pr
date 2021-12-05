# 3pr

    select 

    replace(substr(substr(value, instr(value, '<p>'), instr(value, '</p>')), 0, instr(substr(value, instr(value, '<p>'), instr(value, '</p>')), '</')-1), '<p>') as id,
    replace(substr(substr(value, instr(value, '<h1>'), instr(value, '</h1>')), 0, instr(substr(value, instr(value, '<h1>'), instr(value, '</h1>')), '</h1>')-1), '<h1>') as category,
    case
        when replace(substr(substr(value, instr(value, '<p class="title">')), 0, instr(substr(value, instr(value, '<p class="title">')), '</p>')-1), '<p class="title">') is null
            then trim(replace(substr(substr(value, instr(value, '<p class="author">')), 0, instr(substr(value, instr(value, '<p class="author">')), '</p>')-1), '<p class="author">'))
            else replace(substr(substr(value, instr(value, '<p class="title">')), 0, instr(substr(value, instr(value, '<p class="title">')), '</p>')-1), '<p class="title">')
    end as title,
    case
        when replace(substr(substr(value, instr(value, '<p class="title">')), 0, instr(substr(value, instr(value, '<p class="title">')), '</p>')-1), '<p class="title">') is null
            then null
        when instr(value, '<p class="author">') != 0
            then trim(replace(substr(substr(value, instr(value, '<p class="author">')), 0, instr(substr(value, instr(value, '<p class="author">')), '</p>')-1), '<p class="author">'))
    end as author,
    replace(substr(substr(value, instr(value, '<p class="price">')), 0, instr(substr(value, instr(value, '<p class="price">')), '</p>')-1), '<p class="price">') as price
    from data;
